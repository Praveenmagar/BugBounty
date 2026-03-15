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