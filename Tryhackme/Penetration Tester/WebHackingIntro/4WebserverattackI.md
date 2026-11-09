# Web server Attack I


# Python HTTP Server
- Python has built in HTTP server start with single command
    ```
    python3 -m http.server 8000
    ```
- Developers use it to quickly share files, test static websites, or transfer something between two machines on same network
- Problem "Quickly share files" sometimes becomes "accidentlly exposed to internet for six months", running on public facing servers, internal network shares, and cloud instances where someone opened port 8000 in firewall and forget about it

## What it serves?
- It serves entire working directory, including every file in it like **.env**
- There is no **.htaccess** equivalent, no blocklist, no configuration file
- If file exist in directory, anyone who can reach port 8000 can download it
- Apache or Nginx, directory listing is disabled by default but in Python's HTTP server, it has one mode: serve everything

## Directory listing
- When no **index.html** file is present in directory, Python server generates page listing every file it can see
- Browse 
    ```
    http://machine_ip:8000
    ```
- Curl using
    ```
    curl -s http://machine_ip:8000
    ```

## Accessing Dotfiles
- Dotfiles like **.env** are hidden from normal dirctory navigation on Linux, but Python's server doesn't respect that convention, it serves like other normal file
- **.env** file is common target because developers use it to store environment specific configuration, and that configuration often includes credentials
    ```
    curl -s http://machine_ip:8000/.env
    ```

## Downloading and inspecting archives
- If you see .zip, .tar.gz, or other archive in directory listing, download it and inspect the contents
- Developers sometime leave backup archives in the same directory they are serving which may contain source code, database dumps, or configuration files
    ```
    curl -s http://machine_ip:8000/backup.zip -o backup.zip
    ```
    ```
    unzip backup.zip -d backup-contents/
    ```
    ```
    cat backup-contents/db_dump.sql
    ```

## Why this matters
- Python server is realistic finding because it requires no exploitation
- The misconfiguration is that it is running in a location where it shouldn't be, serving files that shouldn't be public
- If directory shows and **index.html** file instead of showing directory listing, try requesting paths directly or navigating to subdirectories




# Apache2
- Most widely deployed web server in the world, so it nearly appears every engagement that touches web infrastructure
- It's default Ubuntu configuration leaves several things enabled that testers regularly find and report
- Three most common are
    1. Directory listing on specific paths
    2. Server-status module
    3. Backup file sitting in document root

## Version Disclosure
- Check server header
    ```
    curl -SI http://machine_ip:80 | grep -i server
    ```
    - Knowing exact version help you check for known CVEs and understand the server capabilities

## Directory Listing
- Apache's **Options +Indexes** directive tells the server to display a file listing when a directory doesn't have an **index.html** or similar default file
- Browse to
    ```
    http://machine_ip/files/
    ```
- Read every file in it, developers sometimes leave CSV exports, internal notes, or backup files in directories

## The mod_status page
- Apache has built-in status page powered by **mod_status** module
- When configured correctly, it is accessible only from localhost, when misconfigured with **Require all granted**, it is accessible from any IP
- You can access using
    ```
    http://machine_ip:80/server-status
    ```

## Finding unlinked files with Gobuster
- Backup files, old configuration copies, and forgotten test files often sit in the document root with no links pointing to them
- Tools like **Gobuster** discover these by guessing paths against a wordlist
    ```
    gobuster dir -u http://TARGET_IP:80 -w /usr/share/wordlists/SecLists/Discovery/Web-Content/common.txt -x bak,txt,html -t 20
    ```
    - If **.bak** file extension exist, it is always worth retrieving
    - Also pay attention to  **.htpasswd** files
    ```
    curl -s http://machine_ip:80/backup.bak
    ```


# Node.js(Express)
- This application behave differently from Apache and Python HTTP servers
- They are not serving static files from a configured document root
- They are running application code and that code decides what to return for every request
- Attackers look at this because developers often leave development mode features enabled when they push to production

## Framework Fingerprinting
- For **node.js** you will see **X-Powered-By: Express** in the response
    ```
    curl -sI http://machine_ip:3000
    ```
- Express sets this header automatically unless developer explicitly disables it

## Reading the Application Version
- Root path of many Express applications returns JSON status response
    ```
    curl -s http://machine_ip:3000
    ```

## Triggering verbose Errors
- Express built-in error handler suppresses stack traces when **NODE_ENV** is set to **Production**
- In **development** mode, it passes them through
- But developers often write their own error handlers, and those custom handlers expose stack traces regardless of **NODE_ENV**
