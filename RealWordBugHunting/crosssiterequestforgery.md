# Cross-Site Request Forgery(CSRF)
- It occurs when an attacker can make a target browser send an HTTP request to another website
- Attacker able to modify server side information and might even take over a user's account
- **Scenario**
    - Bog login banking website to check balance
    - After finish, Bob check email on different domain
    - Bob has email to unfamiliar website, and click link to see where it leads
    - When loaded, unfamilar site instruct Bob Browser to make http request to Bob banking website, requesting to transfer money from Bob to attacker
    - Banking website receives HTTP request from unfamilar website but lack of CSRF protecting, it processes transfer