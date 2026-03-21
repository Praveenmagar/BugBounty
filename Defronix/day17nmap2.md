# More about NMAP

- Choose one target
- Go and login inside shodan
- Search in shodan
    ```
    hostname:example.com
    ```

- Lets go back to shodan and lets do some filter
    ```
    hostname:example.com -http.title:"Invalid URL"
    ```

- We found one IP now lets recon inside that IP
    - Go inside terminal of linux and check this
        ```
        whois 17.23.45.20
        ```

- Nmap cheatsheet
    ```
    https://www.stationx.net/nmap-cheat-sheet/
    ```

- Now lets run simple nmap command first
    ```
    nmap -sV ipaddress
    ```

    ```
    nmap -sV ipaddress -T4 -A -min-rate 1000 -max-retries 3
    ```

## Where NSE(NMAP Scripting Engine) is located in NMAP
```
cd /usr/share/nmap/scripts
```
- To see NMAP http scripts
    ```
    ls | grep http
    ```
- Or you can also do following
    ```
    ls http*
    ```
- Running nse
    ```
    nmap ipaddress -T4 --script "http-vuln*"
    ```

    ```
    nmap ipaddress -T4 --script "http-*" -vv
    ```

    ```
    locate .nse | grep whois
    ```

    ```
    nmap ipaddress --script whois-ip.nse -vv -T4
    ```

    ```
    ls /usr/share/nmap/scripts/
    ```

    ```
    nmap ipaddress -sV --script "ftp-*" -vv
    ```

# Powerful tool
- Sandmap
    ```
    https://github.com/trimstray/sandmap
    ```
- To execute this

    ```
    sandmap
    ```
    - this open cli for sandbox

    