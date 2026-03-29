# Content Discovery
- Content can be many things, a file, video, picture, backup, a website feature
- Ways for content discovery
    - Manually, 
    - Automated and 
    - OSINT(Open-Source Intelligence)

## Manual Discovery

1. Robots file
    - It is a document that tells search engines which pages they are and aren't allowed to show on their search engine results or ban specific search engines from crawling the website altogether
        ```
         http://MACHINE_IP/robots.txt
        ```

2. Favico 
    - It is a small icon displayed in the browser's address bar or tab used for branding a website
    - When frameworks are used to build a website, a favicon that is part of the installation gets leftover, and if the website developer doesn't replace this with a custom one, this can give us a clue on what framework is in use
    - Download favicon and its md5 hash value
        ```
        curl https://static-labs.tryhackme.cloud/sites/favicon/images/favicon.ico | md5sum
        ```
    - After download see in following database
        ```
        https://wiki.owasp.org/index.php/OWASP_favicon_database
        ```
    
3. Sitemap
    - This file gives a list of every file the website owner wishes to be listed on a search engine
    - It contains areas of the website that are a bit more difficult to navigate to or even list some old webpages that the current site no longer uses but are still working behind the scenes.
        ```
        http://www.example.com/sitemap.xml
        ```

4. HTTP headers
    - Making requests to the web server, the server returns various http headers.
    - These headers can sometimes contain useful information such as the webserver software and possibly the programming/scripting language in use
    - Command to get HTTP headers
        ```
        curl http://MACHINE_IP -v
        ```
        - v means verbose

5. Framework stack
    - After establishing the framework of a website, either from the above favicon or looking the page source such as comments, copyright notices or credits, you can then locate the framework's website.
    - From there, we can learn more about the software and other information, possibly leading to more content we can discover.


## OSINT method
1. Google Hacking/Dorking
    - It utilizes Google's advanced search engine features, which allow you to pick out custom content
    - Examples
        - site
            ```
	        site:tryhackme.com
            ```
        - inurl
            ```
            inurl:admin
            ```
        - filetype
            ```
            filetype:pdf
            ```
        - intitle
            ```
            intitle:admin
            ```