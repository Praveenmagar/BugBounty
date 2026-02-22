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