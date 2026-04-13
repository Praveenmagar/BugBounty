# Scanning the network
 
## Divided into following section
1. Open Source Intelligence, 
2. External Scanning,
3. Internal Scanning, and 
4. Web Application Scanning


## Open Source Intelligence (OSINT)- Passive Discovery
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
        http://72.61.245.140:5001
        ```

