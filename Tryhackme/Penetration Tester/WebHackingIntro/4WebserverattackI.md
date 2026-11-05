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