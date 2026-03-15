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

- In same subnet, expect scanner to use ARP Address Resolution Protocol (ARP) queries to discover live hosts.
## ARP scan only possible in same subnet
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

## Discovering live hosts
- ARP from Link Layer
- ICMP from the Network Layer
- TCP from the Transport Layer
- UDP from the Transport Layer

### ARP
- Send frame to the broadcast address on the network segment and asking the computer with a specific IP address to respond by providing its MAC address

### ICMP
- It has many types. 
- ICMP ping uses Type 8 (Echo) and Type 0 (Echo Reply).
- To ping on the same subnet, an ARP query should precede the ICMP Echo.

### TCP & UDP
- For network scanning, a scanner can send a specially crafted packet to common TCP or UDP ports to check whether the target responds. 
- This method is efficient, especially when ICMP Echo is blocked

### Nmap host discovery using ARP
- Privileged user scan on local network(Ethernet), Nmap uses ARP request
- Privileged user on outside local network, Nmap uses ICMP echo request, TCP ACK to port 80, TCP SYN to 443 and ICMP timestamp request
- Unprovileged user on outside local network, Nmap resorts to TCP three way handshake

**NMAP bydefault uses ping scan to find live hosts**

- **Nmap to discover online hosts without port scanning live system**
    ```
    nmap -sn TARGETS
    ```

## To get MAC address, OS send ARP query

- **to perform an ARP scan without port-scanning**
    ```
    nmap -PR -sn TARGETS
    ```
    - PR means you only want ARP scan
    ```
    nmap -PR -sn MACHINE_IP/24
    ```
