# Part One

- To enable logging
    - This becomes very useful for bulk attack/queries or if your client requires these logs
        ```
        echo "spool /home/kali/msf_console.log" > ~/.msf4/msfconsole.rc
        ```
    - Now open msfconsole and run some commands
        ```
        help
        ```
        ```
        ls
        ```
        ```
        show options
        ```
    - and check
        ```
        cat /home/kali/msf_console.log
        ```
    - You will find the msfconsole logged content
    - If you want to run msfconsole as root then above will not keep log of it so you need to make it in the form of root but only few required root access in msfconsole
    - Root access requird
        - Privileged ports (<1024)
        - Network sniffing
        - ARP spoofing / MITM
        - Some exploits requiring raw sockets
    - For root access use
        ```
        sudo mkdir -p /root/.msf4
        echo "spool /root/msf_console.log" | sudo tee /root/.msf4/msfconsole.rc
        ```

## Tools used
1. Donut
    - Convert EXE/DLL into shellcode so it can be executed in memory instead of from disk
    - How to run?
        ```
        cd donut
        ```

        ```
        ./donut -i test.exe -f 1 -o shellcode.bin
        ```
    - Used in place of The Backdoor Factory

2. gowitness (Used in place of HTTPScreenShot)
- Go to github
    ```
    https://github.com/sensepost/gowitness
    ```
- Use following command
    ```
    go install github.com/sensepost/gowitness@latest
    ```
- This install in specific location that is
    ```
    ~/go/bin/gowitness
    ```
- To make it accessible in everywhere you have to adjust path
    ```
    echo 'export PATH=$PATH:$HOME/go/bin' >> ~/.zshrc
    source ~/.zshrc
    ```
- Now you can access it from everywhere using
    ```
    gowitness
    ```

3. SMBExec
- Use below command to execute
    ```
    sudo apt update
    sudo apt install git python3-pip pipx -y
    git clone https://github.com/fortra/impacket.git
    cd impacket
    pipx install .
    ```
    