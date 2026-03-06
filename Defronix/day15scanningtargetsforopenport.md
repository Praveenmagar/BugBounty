# Scanning target for Open ports

- **Why Scanning?**
    - For possible IP addresses with open ports and more domains from those IP addresses.

- Now lets scan one target
    ```
    nmap cybertechschool.com
    ```
- for more detail scan
    ```
    nmap cybertechschool.com -sV
    ```
- You will get service with their version and now check for its exploit in terminal
    ```
    searchsploit  OpenSSH 9.6p1
    ```
- You can search same thing in google also
    ```
    OpenSSH 9.6p1 exploit
    ```


## Our tasks
- To collect as many IP addresses of a target
- Do a port scan and find services and open ports and look for possible bugs
- Do a reverse DNS- to convert IP to domain
- Find some juice info/bug

**When we talk about IP then we need to go for bigger task because smaller company will have small IP blocks**
- Some sites to know about bigger company IP range
    ```
    https://whois.arin.net/
    ```
    ```
    https://bgp.he.net/
    ```
    - this bgp.he.net also help to find asn number


- Now find the asn number from bgp.he.net and go to shodan and try to search it
    ```
    asn:AS394161 http.status:200
    ```

- If you get login panel then you can do bruteforce attack using username and password by using burpsuite tool
- In Burpsuite
    - Capture login page by Burpsuite by using simple admin and admin as username and password.
    - Send capture file to intruder
    - Go to position and select cluster bomb
    - Go to payloads




# What can you do with the help of ASN number?
- We can find CIDR(IP range) block


- Next proper graphical tool to use ASN number
    ```
    https://mxtoolbox.com/SuperTool.aspx
    ```
    - mxtoolbox. Here, go to supertool button
    - In supertool search bar put asn number value and select ASN lookup to search total number of IPs


- **Tool to find IP address range**
- One popular tool from project discovery
    ```
    https://github.com/projectdiscovery/asnmap
    ```
- use go to install it
- After installing set API key and run following
    ```
    asnmap -a AS714
    ```


# Lets work on one target

## First Step: Finding CIDR range
- Go to bgp.he.net and find ASN number of apple
- Go to attacker machine and create one apple folder
    ```
    mkdir apple
    ```
- Go inside it
    ```
    cd apple
    ```
- Run following command inside it
    ```
    asnmap -a AS714 > applecidr.txt
    ```

## Second step: Finding IP from CIDR range
- One popular tool mapcidr
    ```
    https://github.com/projectdiscovery/mapcidr
    ```
- command to find ip
    ```
    mapcidr -cidr applecidr.txt
    ```
- Scanning single range
    ```
    mapcidr -cidr 17.0.0.0/18
    ```
- Storing single CIDR range value IPs in file
    ```
    mapcidr -cidr 17.0.0.0/18 -o appleips.txt
    ```

## Third step: Checking IP with open ports
- Download that appleips.txt inside host machine and we have different tools to check which ip have open ports and many more
- In window we have AngryIp scanner tool


## Fourth step: Finding domain name from IP
- Tools used dnsx from project discovery
    ```
    https://github.com/projectdiscovery/dnsx
    ```
- to install
    ```
    go install -v github.com/projectdiscovery/dnsx/cmd/dnsx@latest
    ```
- command to run
    ```
    echo 17.0.0.0/18 | mapcidr -silent | dnsx -ptr -resp-only
    ```
    - Here ptr responsible to convert ip to domain

    ```
    mapcidr -cidr applecidr.txt | dnsx -ptr -resp-only
    ```

    ```
    subfinder -silent -d hackerone.com | dnsx -silent  -asn
    ```


## Another tool is naabu
```
https://github.com/projectdiscovery/naabu
```
- To install
    ```
    go install -v github.com/projectdiscovery/naabu/v2/cmd/naabu@latest
    ```
- To run
    ```
    naabu -h
    ```
    ```
    naabu -host apple.com
    ```
    ```
    naabu -host apple.com -tp 1000
    ```
    ```
    naabu -l appleips.txt
    ```

## MASSCAN: another powerful tool
```
https://github.com/robertdavidgraham/masscan
```
