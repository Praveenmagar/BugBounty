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

    - this open cli for sandbox
    ```
    sandmap
    ```

    - to see modules
    ```
    list
    ```

    - to clear content
    ```
    clear
    ```

    - To see module info
    ```
    show port_scan
    ```

    - To use port_scan
    ```
    use port_scan
    ```

    - To see its content
    ```
    show
    ```

    - To set target ip
    ```
    set dest ipaddress
    ```

    - To execute task
    ```
    init null_scan
    ```
    OR
    ```
    init 4
    ```

    - To go back type
    ```
    main
    ```

    - To use service detection
    ```
    use service_detection
    ```

    - To see
    ```
    show
    ```

    - To set target
    ```
    set dest ipaddress
    ```

    - To execute action
    ```
    init 1
    ```


- Next Tool 
    - Scancannon
        ```
        https://github.com/johnnyxmas/ScanCannon
        ```
    