# Subdomain Enumeration

- Process of finding valid subdomains for a domain

## Different Enumeration methods

1. OSINT-SSL/TLS certificates
    - Publicly accessible logs of every SSL/TLS certificate created for a domain name
    - The purpose of Certificate Transparency logs is to stop malicious and accidentally made certificates from being used
    - Sites used
        ```
        https://crt.sh/
        ```
    - How to search?
        ```
        example.com
        ```
    - Dont use https://www.example.com

2. OSINT-Search engine
    - Search engines contain trillions of links to more than a billion websites, which can be an excellent resource for finding new subdomains
        ```
        site:*.domain.com -site:www.domain.com
        ```

3. DNS Bruteforce
    - It is the method of trying tens, hundreds, thousands or even millions of different possible subdomains from a pre-defined list of commonly used subdomains
    - Many tools are there like DNS recon

4. OSINT sublist3r
    - To speed up the process OSINT of subdomain discovery, we can automate the above methods with the help of tools like Sublist3r

5. Virtual Host
    - Some subdomains aren't always hosted in publically accessible DNS results, such as development versions of a web application or administration portals. 
    - Instead, the DNS record could be kept on a private DNS server or recorded on the developer's machines in their /etc/hosts file (or c:\windows\system32\drivers\etc\hosts file for Windows users), which maps domain names to IP addresses. 
    - Web servers can host multiple websites from one server when a website is requested from a client, the server knows which website the client wants from the Host header.
        ```
        ffuf -w /usr/share/wordlists/SecLists/Discovery/DNS/namelist.txt -H "Host: FUZZ.acmeitsupport.thm" -u http://MACHINE_IP
        ```
    - OR
        ```
        ffuf -w /usr/share/wordlists/SecLists/Discovery/DNS/namelist.txt -H "Host: FUZZ.acmeitsupport.thm" -u http://MACHINE_IP -fs {size}
        ```