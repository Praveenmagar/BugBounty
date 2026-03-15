# Nmap for Bug bounty

- used for
    - Enumeration
    - Host discovery
    - Find open Ports
    - Service and version detection
    - OS detection

- Ways for Host Discovery
    - Using ARP request packet
    - Sending TCP packet
    - Sending UDP packet
    - Sending ICMP packet


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

- In same subnet, expect scanner to use ARP Address Resolution Protocol (ARP) queries to discover live hosts.
- ARP query aims to obtain the hardware address (MAC address) so that communication at the link layer
becomes possible

- To scan list of target
    ```
    nmap -iL list_of_hosts.txt
    ```
- To check list of host nmap will scan
    ```
    nmap -sL TARGETS
    ```
- **How many IP addresses will Nmap scan if you provide the following range 10.10.0-255.101-125?** 
    ```
    nmap -sL 10.10.0-255.101-125
    ```

- **What is the first IP address Nmap would scan if you provided 10.10.12.13/29 as your target?**
    ```
    nmap -sL -n 10.10.12.13/29
    ```