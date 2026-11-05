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