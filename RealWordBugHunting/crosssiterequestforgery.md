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