# Cross Site Scripting(XSS)

- To execute JavaScript payload on web applications with an intention to execute those without proper input validation by the web application

    ```
    <script>alert("hello")</script>
    ```

- **How to find XSS?**
    - At any search form or input form run following
        ```
        <script>alert("hello")</script>
        ```
        
    - Go for different parameters in url
    
# XSS types
- Reflected XSS
- Stored XSS
- DOM XSS
- Blind XSS
