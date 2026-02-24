# Cross-Site Request Forgery(CSRF)
- It occurs when an attacker can make a target browser send an HTTP request to another website
- Attacker able to modify server side information and might even take over a user's account
**Scenario**
    - Bog login banking website to check balance
    - After finish, Bob check email on different domain
    - Bob has email to unfamiliar website, and click link to see where it leads
    - When loaded, unfamilar site instruct Bob Browser to make http request to Bob banking website, requesting to transfer money from Bob to attacker
    - Banking website receives HTTP request from unfamilar website but lack of CSRF protecting, it processes transfer

**Authentication**
- Two ways to store authentication
    - Basic authentication Protocol
    - Using cookie

- **Basic authentication**
    - Uses base64-encoded username and password seperated by colon
```text
Authorization: Basic QWxhZGpbjpPcGVuV----
```
- Here if we decode, QWxhZGpbjpPcGVuV---- contains username and Password seperated by colon
```text
QWxhZGpbjpPcGVuV---- = Aladdin:OpenSesame
```
 - Aladdin= Username
 - OpenSesame= Password

- **Using Cookie**
    - It is small file website create and store in User's browser
    - Cookie attributes
        - Domain
        - Expires: tell browser to destroy cookie on specific date
        - Max-age: number of second until cookie expire
        - Secure: send cookie only in https site
        - httponly: read cookie only through http and https, Js can't read it
    - Single site set 50 to 150 cookies in common browser
    - Some support upto 600 cookies
    - Browser allow 4KB per cookie
    - Website uses cookie named sessionId to remember user rather than username and password

## CSRF With GET REQUEST
- If bank accept transfer via GET request, malicious site send http request with either hidden form or <img> tag
- When browser render <img> tag it makes HTTP GET request to src attributes and include any existing cookie in that request
- Malicious <img> tag using fake URL as its source
```text
<img src="https://www.bank.com/transfer?from=bob&to=Joe&amount=5000">
```
- when Bob visits attacker owned site having <img> tag in its response, browser make HTTP GET request to bank

**Solution**
- Avoid HTTP GET request on backend
- Use POST with CSRF protection


**CSRF with POST**
- <img> tag won't work here only from work
- **Simple situation**
- POST request with content-type 
    - application/x-www-form-urlencoded
    - text/plain
```text
POST / HTTP/1.1
Host: www.google.ca
User-Agent: Mozilla/5.0 (Windows NT 6.1; rv:50.0) Gecko/20100101 Firefox/50.0
Accept: text/html, application/xhtml+xml, application/xml;q=0.9,*/*; q=0.8
Content-Length: 5
Content-Type: text/plain; charset=UTF-8
DNT: 1
Connection: close
hello
```
- Content-type is important because browser treat types differently
- In above content-type, it's possible for malicious site to create hidden HTML form and submit silently to the vulnerable site without target's knowledge
- Form can submit post or get request to URL and can even submit paramete value
```text
<iframe style="display:none" name="csrf-frame"></iframe>
<form method='POST' action='http://bank.com/transfer' target="csrf-frame" id="csrf-form">
<input type="hidden" name="from" value="bob">
<input type="hidden" name="to" value="Joe">
<input type="hidden" name="amount" value="5000">
<input type="submit" value="Joe">
</form>
<script>document.getElementById("csrf-form").submit()</script>
```
- Once the form is submitted, browser make POST request to send Bob's cookies to bank site, which invokes transfer
- POST request send HTTP response back to browser, the attacker hide response in iFrame using "display:none"

**Other Scenario**
- Site might expect POST request to be submitted with content-type application/json
- some cases request with application/json type have CSRF token
- Sometime HTTP body of POST request has token
- Sometime POST request has custom header with name like X-CSRF-Token
- Browser send OPTIONS HTTP request before POST request site respond to OPTION call indicating types of HTTP requests it accepts and from which trusted origins(this is referred as preflight OPTIONS)
- The sets of rules defining when and how website can read responses from each other is called Cross Origin resource sharing(CORS)
- You can't submit application/json request, unless site being tested allow it

**Some Cases**
- You can bypass these protections by changing content-type to
    - application/x-www-form-urlencoded
    - multipart/form-data
    - text/plain
- Browser don't send preflight OPTION call for any of them when making POST request


**PROTECTION OF CSRF**
- CSRF TOKEN
    - web app generate token in two parts
        - One Bob would receive
        - One application retain
    - When Bob attempt to make transfer request, he have to submit his token, which bank validate with its side of token
    - Some names of token are X-CSRF-TOKEN, Lia-Token, rt or form-id
    - Token can be included in
        - HTTP request header
        - HTTP POST body
        - hidden field
```text
<form method='POST' action='http://bank.com/transfer'>
<input type="text" name="from" value="bob">
------------------------------------------
------------------------------------------
<input type="hidden" name="csrf" value="1Ht7DDyVUNKo----------">
```
- **Try removing token, change its value and so on to conform token has been implemented properly**


- USING CORS
    - This isn't fullproof because it relies on browser security and ensuring proper CORS
    - Sometimes bypass CORS by changing content-type
        - application/json to application/x-www-form-urlencoded
        - use GET request instead of POST
    - **Browser send OPTION HTTP automatically if content-type is application/json but won't send automatically if it's GET request or content-type is application/x-www-form-urlencoded**


**Other less effective methods**
- Check value of Origin or Referer header submitted
- Browser start to support a new cookie attributes called samesite. Samesite can be  set strict or lax


**Example**
- **SHOPIFY TWITTER DISCONNECT**
    - For potential CSRF vulnerability look for GET request that modify server-side data
    ```
    https://twitter-commerce.shopifyapps.com/auth/twitter/disconnect/
    ```
    - Shopify was not validating legitimacy of GET request sent to it making URL vulnerable to CSRF
    ```
    <html>
    <body>
        <img src="https://twitter-commerce.shopifyapps.com/auth/twitter/disconnect">
    </body>
    </html>
    ```
    - To find this vulnerability
        - Use proxy server like Burp or OWASP's ZAP to monitor HTTP request
