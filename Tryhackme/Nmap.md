# Nmap

- Nmap Live Host Discovery
- Nmap Basic Port Scans
- Nmap Advanced Port Scans
- Nmap Post Port Scans


# Nmap Live Host Discovery
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

# Nmap host discovery using ARP
- Privileged user scan on local network(Ethernet), Nmap uses ARP request
- Privileged user on outside local network, Nmap uses ICMP echo request, TCP ACK to port 80, TCP SYN to 443 and ICMP timestamp request
- Unprovileged user on outside local network, Nmap resorts to TCP three way handshake

**NMAP bydefault uses ping scan to find live hosts**

- **Nmap to discover online hosts without port scanning live system**
    ```
    nmap -sn TARGETS
    ```

**To get MAC address, OS send ARP query**
**A host that replies to ARP queries is up**

- **to perform an ARP scan without port-scanning**
    ```
    nmap -PR -sn TARGETS
    ```
    - PR means you only want ARP scan
    ```
    nmap -PR -sn MACHINE_IP/24
    ```

## ARP scan tool
- provides many options to customise your scan
- send ARP queries to all valid IP addresses on your local networks
    ```
    arp-scan --localnet
    ```
- OR
    ```
    arp-scan -l
    ```

- Among multiple interface, you want to scan only one
    ```
    sudo arp-scan -I eth0 -l
    ```
- To scan subnet
    ```
    sudo arp-scan 10.10.210.6/24
    ```

##  we can see using tcpdump, Wireshark to see ARP Query


# Host discovery using ICMP
- Ping every IP address on a target network and see who would respond to our ping (ICMP Type 8/Echo) requests with a ping reply (ICMP Type 0)
- New windows uses host firewall to block ICMP echo bydefault
- **ARP query precedes an ICMP request if your target is on the same subnet**
- ICMP echo request to discover live hosts
    ```
    nmap -PE -sn MACHINE_IP/24
    ```
- Scanning above in same or different subnet result will be same with only one difference
    - Same subnet: result with MAC address
    - Different subnet: result without MAC address

    ![Screenshot](../images/nmapicmp.png)

- Result in wireshark
    ![Screenshot](../images/nmapicmpwireshark.png)

- Mostly ICMP is blocked, So try ICMP timestamp request (ICMP Type 13) and with Timestamp reply (ICMP Type 14)
    ```
    nmap -PP -sn target_ip/24
    ```

    ![Screenshot](../images/nmapicmptimestamp.png)

    ![Screenshot](../images/nmapicmptimewireshark.png)

-  mask queries (ICMP Type 17) and checks whether it gets an address mask reply (ICMP Type 18)

    ![Screenshot](../images/nmapicmpmask.png)

    ![Screenshot](../images/nmapicmpmaskwiresh.png)


## Host discovery using TCP and UDP
- **TCP SYN Ping**
    - open port reply SYN/ACK (Acknowledge)
    - closed port reply RST (Reset)
        ```
        nmap -PS -sn MACHINE_IP/24
        ```
    - Privileged user: No three way TCP handshake for open port
    - Unprivileged user: Require three way TCP handshake

- **TCP ACK Ping**
    - Must be privileged user for this.
    - For unprivileged user, need attempt a 3-way handshake.
        ```
        sudo nmap -PA -sn MACHINE_IP/24
        ```
    
- **UDP ping**

    ![Screenshot](../images/udpping.png)

## MASSSCAN
- uses a similar approach to discover the available system
    ```
    masscan MACHINE_IP/24 -p443
    ```

    ```
    masscan MACHINE_IP/24 -p80,443
    ```

    ```
    masscan MACHINE_IP/24 -p22-25
    ```

    ```
    masscan MACHINE_IP/24 ‐‐top-ports 100
    ```

# Some important options
- no DNS lookup 
    ```
    -n
    ```
- Reverse DNS lookup for all hosts
    ```
    -R
    ```
- host discovery only
    ```
    -sn
    ```


# Nmap Basic Port Scans

## TCP flags

![Screenshot](../images/tcpflags.png)

- URG 
    - Urgent pointer indicates incoming data is urgent, and processed immediately without consideration of having to wait on previously sent TCP segments
- ACK 
    - acknowledge the receipt of a TCP segment.
- PSH: 
    - Ask TCP to pass the data to the application promptly.
- RST: 
    - Used to reset the connection. 
    - firewall, might send it to tear a TCP connection. 
    - used when data is sent to a host and there is no service on the receiving end to answer.
- SYN: 
    - Used to initiate a TCP 3-way handshake and synchronize sequence numbers with the other host. 
    - Sequence number should be set randomly during TCP connection establishment.
- FIN: 
    - The sender has no more data to send.

## TCP connect Scan
- Learning whether the TCP port is open, not establishing a TCP connection. Hence the connection is torn as soon as its state is confirmed by sending a RST/ACK. You can choose to run TCP connect scan using -sT.

    ![Screenshot](../images/tcpopen.png)

- For non-privileged user, a TCP connect scan is the only possible option to discover open TCP ports.

- TCP SYN flag set to various ports, 256, 443, 143, and so on.
- By default, Nmap will attempt to connect to the 1000 most common ports. 
- Closed TCP port responds to a SYN packet with RST/ACK to indicate that it is not open.

    ![Screenshot](../images/tcpscanwireshark.png)

- Here, port 143 open, so it replied with a SYN/ACK, and Nmap completed the 3-way handshake by sending an ACK.
- Then, the fourth packet tears it down with an RST/ACK packet.

    ![Screenshot](../images/tcpthreeway.png)
