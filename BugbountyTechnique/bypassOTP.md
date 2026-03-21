# How to bypass OTP

- At first find urls
    ```
    echo example.com | waybackurls | tee allurls.txt
    ```
- Next lets use python xsstrike.py  
    - It is cross site Scripting detection suite
        ```
         python3 /root/XSStrike/xsstrike.py -h
        ```
    - To execute it
        ```
         python3 /root/XSStrike/xsstrike.py -u https://www.instafinancials.com/ --crawl
        ```
- Now goto burpsuite and capture the packet and try to manipulate it

- Run following command in terminal using nuclei
    ```
    nuclei -l all-urls.txt -t ../nuclei-templates/
    ```