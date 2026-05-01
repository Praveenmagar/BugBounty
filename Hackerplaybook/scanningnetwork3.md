# Scanning the network
 
## Divided into following section
1. Open Source Intelligence, 
2. External Scanning,
3. Internal Scanning, and 
4. Web Application Scanning


# Open Source Intelligence (OSINT)- Passive Discovery
- Tools
    1. Recon-NG: Not so relevant 

    2. Lee Baird
    - This will not work as root so i clone and run this in my vmware linux not in my VPS
        ```
        git clone https://github.com/leebaird/discover.git
        ```

        ```
        cd discover
        ```

        ```
        ./discover.sh
        ```

    3. Spider foot
    - How to install it
        ```
        cd Hackerplaybook
        git clone https://github.com/smicallef/spiderfoot.git
        cd spiderfoot

        python3 -m venv venv
        source venv/bin/activate

        pip install -r requirements.txt

        python3 sf.py -l 127.0.0.1:5001
        ```
    - But running like for VPS will not work because VPS has no graphical interface so instead of this
        ```
        python3 sf.py -l 127.0.0.1:5001
        ```
    - Use this
        ```
        python3 sf.py -l 0.0.0.0:5001
        ```
    - Here 0.0.0.0 means accessible from anywhere. So now use this URL in your local or host browser
        ```
        http://VPS_IP:5001
        ```
    - How to set password in Spider Foot?
        ```
        mkdir -p /root/.spiderfoot
        ```
        ```
        nano /root/.spiderfoot/passwd
        ```
        ```
        praveen:1234
        ```
        - Where Username= praveen and password= 1234
        ```
        python3 sf.py -l 0.0.0.0:5001
        ```
        - Go to your local machine
        ```
        http://VPS_IP:5001
        ```


#### Creating Password List
- Finding more targeted information about the company, the people, the location, and their customers by developing more customized password list
- Creating custom and smart word lists based on our victim companies and related industries

**How to create best password list?**
1. Understand the Target (MOST IMPORTANT)
    - Start with OSINT:
        - Website pages, About section, Careers page, Blog posts
    - Extract: 
        - Product names, Internal terms, Departments, Technologies

2. Use CeWL
    ```
    sudo apt install cewl
    ```
    ```
    cewl https://company.com -d 2 -w words.txt
    ```
3. Extract word from JS files
    ```
    curl -s https://company.com/app.js | grep -oE "[a-zA-Z0-9_/.-]+" | sort -u
    ```
4. Use GitHub Dorking (GitDorker)
    ```
    company.com password
    company.com api
    company.com secret
    ```
5. Manual Intelligence (VERY UNDERRATED)
    - Look at: LinkedIn employees, Job descriptions

**Small but smart wordlist > big but random wordlist**

- Tools
    1. Wordhound: not relevant today use cewl instead
    2. BruteScrape: not relevant use cewl instead


#### Using Compromised Lists To Find Email Addresses And Credentials
- Being a penetration tester you have to get creative and use all sorts of resources, just as if someone was malicious. 
- One tactic: using known credential dumps for password reuse
- Search using Linux grep
    ```
    nano file.txt
    ```

    ```
    user1@yahoo.com:hash123
    user2@company.com:hash456
    admin@company.com:hash789
    ```

    ```
    grep "@company.com" file.txt
    ```

#### Github - Analysis
1. Gitrob: it is already outdated. So other relevant tools are
    1. Trufflehog
    2. Gitdorker
    3. Gitleaks
    


# External/Internal Active Discovery

- **One of most effective scanning steps**
    1. Scanning with Masscan
        -  Historically, we have all used nmap to map out IPs/Ports, but the game has been changing
        -  Large ranges are a pain to scan, but this is where Masscan comes into play
            ```
            masscan -p0-65535 23.239.151.0/24 --rate 150000 -oL output.txt
            ```
        - Try to run same scan with nmap
            ```
            nmap -v -PN -n -sT -T5 23.239.151.0/24 -p0-65535 -oN output_nmap.txt
            ```
        - Masscan improves scanning significantly and allows a tester to scan and have results in minimal time
        - Feature to configure your Masscan scans: --echo switch
            ```
            /masscan -p0-65535 23.239.151.0/24 --rate 150000 -oL output.txt --echo > scan.conf
            ```
            ```
            cat scan.conf
            ```

    2. Scanning with sparta: it is already outdated so lets replace it with Legion
        - Legion is bydefault installed inside kali linux. So here i am using vmware linux
        - Always rung legion with  sudo
            ```
            sudo legion
            ```
    3. Scanning with httpscreenshot: it is already outdated. So replace with
        - gowitness
        - aquatone

    - **Best Workflow for Scanning**
        - Scan target
            ```
            masscan 192.168.1.0/24 -p80,443,8080,8443 --rate=1000 -oG masscan.txt
            ```
        - Extract required data
            ```
            grep open masscan.txt | awk '{print $2}' | sort -u > ips.txt
            ```
        - Check live url
            ```
            cat ips.txt | httpx -ports 80,443,8080,8443 -silent > web.txt
            ```
        - Take Screenshot
            ```
            gowitness scan file -f web.txt
            ```
    
    #### Vulnerability Scan
    - After performing initial scans and mapping out the network, I usually like to kick off a couple of vulnerability scans in the background
    - Tools
        1. Rapid7 Nexpose
        2. Tenable Nessus
        3. OpenVAS
            - I have install OpenVAS in kali linux vmware. To open this go to linux and type
                ```
                sudo gvm-start
                ```
            - and open the following URL
                ```
                https://127.0.0.1:9392
                ```
            - and put the username as admin and put password 


# Web application Scanning
- After I start the network scanners and get a layout with the active discovery tools, I begin my web
application scanners
- There are lot of open source tools for web scanning like
    - ZAP, 
    - WebScarab, 
    - Nikto, 
    - w3af
- But we are going for Burpsuite

    #### The Process For Web Scanning
    - Spider/Discovery/Scanning with Burp Pro
    - Scanning with a web application scanner
    - Manual parameter injection
    - Session token analysis

- After running a tool like Nessus or Nexpose to find the common system/application/service
vulnerabilities, it is time to dig into the application
- Content Discovery
    - Go to target
    - sitemap
    -  URL view
    - Right click in url and go to engagement tool
    - Select content discovery
    - click on the "Session is not running" button and the application will start "smart brute forcing" folders
    
 
 # The Drive - Exploiting Scanner Findings

 #### 1. Metasploit

 #### 2. Scripts
    - Many exploits for vulnerabilities are not in Metasploit
    - Scripts/codes will be written in Python, C++, Ruby, Perl, Bash, or some other type of scripting language
    - As a penetration tester, you need to be familiar with how to edit, modify, execute, and understand the scripts/codes regardless of the language and be able to understand why an exploit works

**Note: Always execute script only after testing because After the script exploits the vulnerability, the payload deletes everything on the vulnerable host**

#### 3. Printers
- Going from low to owning the network. Favorite examples is printers mainly multi-function printers(MFP)


## Nosqlmap


## Elastic search
- I have installed it in vmware kali linux
- At first 
    ```
    cd ~/elastic-lab
    ```
- Now start it
    ```
    docker-compose up -d
    ```
- To stop server
    ```
    docker-compose down
    ```
- After starting check status
    ```
    docker ps
    ```

- After starting go to browser and type for elastic search
    ```
    http://localhost:9200
    ```
- You can verify it using curl
    ```
    curl http://localhost:9200
    ```
- For Kibana
    ```
    http://localhost:5601
    ```

page 127