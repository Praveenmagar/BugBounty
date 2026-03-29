# File Inclusion

- It includes 
    1. Local File Inclusion (LFI), 
    2. Remote File Inclusion (RFI), and 
    3. directory traversal.

-  For example, if a user wants to access and display their CV within the web application, the request may look as follows, :http//example.com/get.php?file=userCV.pdf, where the file is the parameter and the userCV.pdf, is the required file to access.

    ![Screenshot](/images/fileinclusion.png)

- Commonly found and exploited in various programming languages for web applications, such as PHP that are poorly written and implemented

- Risks
    - Leak data, such as code, credentials or other important files related to the web application or operating system.
    - Moreover, if the attacker can write files to the server by any other means, file inclusion might be used in tandem to gain remote command execution

1. Path Traversal
    - Also known as Directory traversal, a web security vulnerability allows an attacker to read operating system resources, such as local files on the server running an application. 
    - The attacker exploits this vulnerability by manipulating and abusing the web application's URL to locate and access files or directories stored outside the application's root directory

        ![Screenshot](/images/pathtraversal.png)

    - Moving the directory one step up using the double dots ../
    - Path directory

        ![Screenshot](/images/pathtraversal1.png)
    
    - attacker can try the following depending on the target OS version:
        ```
        http://webapp.thm/get.php?file=../../../../boot.ini
        ```
    - OR
        ```
        http://webapp.thm/get.php?file=../../../../windows/win.ini
        ```

        ![Screenshot](/images/pathtraversal2.png)