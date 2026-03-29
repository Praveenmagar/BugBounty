# Insecure Direct Object Reference

- It is a type of access control vulnerability
- It can occur when a web server receives user-supplied input to retrieve objects (files, data, documents), without validation on the server-side to confirm the requested object belongs to the user requesting it

- Example
    - Your link is 
        ```
        http://example.com/profile?user_id=1305
        ```
    - With curosity you try to chang id number
        ```
        http://example.com/profile?user_id=1500
        ```
    - and you get details of another user this is IDOR

1. Finding IDOR in Encoded IDs
    - Passing data from page to page developer often encode raw data
    - Most common encoding is base64 which can be decode using
        ```
         https://www.base64decode.org/  
         ```
    - and can re-encode using
        ```
        https://www.base64encode.org/ 
        ```

2. Finding IDOR in hashed value
    - Little bit more complicated to deal with than encoded ones, but they may follow a predictable pattern, such as being the hashed version of the integer value
    - Can be decoded using
        ```
        https://crackstation.net/
        ```

3. Finding IDOR in unpredicted IDs
    - If the Id cannot be detected using the above methods, an excellent method of IDOR detection is to create two accounts and swap the Id numbers between them.
    - If you can view the other users' content using their Id number while still being logged in with a different account (or not logged in at all), you've found a valid IDOR vulnerability