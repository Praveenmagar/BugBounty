# Nmap for Bug bounty

- used for
    - Enumeration
    - Host discovery
    - Find open Ports
    - Service and version detection
    - OS detection

- **States of Port**
    - Open
        - Some service is running
    - Close
        - No service
    - Filtered
        - nmap doesn't know it is close or open due to firewall
    - Unfiltered
        - port is accessible but nmap doesn't know whether port is open or close
    - Open|filtered
        - nmap doesn't know open or filtered
    - Close|filtered
        - nmap doesn't know close or filtered

## Finding live host
- ARP
- ICMP
- TCP
- UDP

- -sn disable port scanning, only host scan
- -Pn disable host discovery. Port scan only
# Scanning in IP
- To scan list of target
    ```
    nmap -iL list_of_hosts.txt
    ```
- To check list of host nmap will scan
    ```
    nmap -sL TARGETS
    ```
    ```
    nmap -iL list_of_hosts.txt -sn -vv -T5
    ```

## Lets scan in Live domains

```
nmap -iL list_of_domains.txt -sn -PR
```
- Note: All domains should be without http like www.example.com

## Scanning single IP
```
nmap 201.323.10.45 -Pn -sV -T4 -vv
```
```
nmap -sV -T4 57.103.5.194 -vv -p 0-65535 -Pn
```