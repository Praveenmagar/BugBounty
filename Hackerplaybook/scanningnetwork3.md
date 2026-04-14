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