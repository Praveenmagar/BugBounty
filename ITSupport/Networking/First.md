# Networking

## MAC: Physical address, asigned by manufacturer
## IP: Logical address, assigned by administrator or by dedicated service

## Do we have IP address in brand new computer?
- Yes, every brand new computer has IP address range from(169.254.0.1- 169.254.255.254)
- This is called APIPA(Automatic Private IP addressing)
- Two mode of IP assign: Manual and Dynamic
- Bydefault every computer has Dynamic mode on
- It is a Windows and OS fallback feature that automatically assigns a local IP address (169.254.x.x) when a device cannot reach a DHCP server

# Questions
1. Your client call and say he/she is not able to go online and everyone other is online?
- First: Create ticket :Manish can't go online
- Being L1 support you don't have access to server
- So, try to do basic troubleshoot and if it don't work escalate it to L2 support
- Go to cmd and type
    ```
    ipconfig /release
    ```
    - This make ip 0.0.0.0
- Type
    ```
    ipconfig /renew
    ```
    - Asking DHCP for IP address
- Now, ask client is it working
- Client, yes
- Resolved. Closed ticket

## Classes of IP
1. Class A: 1-126
2. Class B: 128-191
3. Class C: 192-223
4. Class D: 224-239(multicasting)
5. Class E: 240-255(Research and experiment)

## In Each class there is
1. Network ID and Host ID
2. In each class first IP is network id which identify network and last IP is broadcast IP to delivery message through entire network at same time
3. For class C IP 202.5.16.0: 
    - Network id is 202.5.16.0
    - IP address range: 202.5.16.1- 202.5.16.254
    - Broadcast ID: 202.5.16.255
4. For Class B
    - 172.16.0.0: Network ID
    - First IP: 172.16.0.1
    - Last valid IP: 172.16.255.254
    - Range: 172.16.0.1- 172.16.255.254
    - Broadcast IP: 172.16.255.255
5. For class A
    - 10.0.0.0: Network ID
    - IP range: 10.0.0.1- 10.255.255.254
    - Broadcast IP: 10.255.255.255
    