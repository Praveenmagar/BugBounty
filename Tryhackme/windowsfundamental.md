# Windows Fundamental
- What encryption can you enable in Pro that can't be enable in home?
    - Bitlocker

- **File System**
    - Modern window use New Technology File System(NTFS)
    - Before NTFS
        - FAT16/FAT32(File Allocation Table)
        - HPFS(High Performance File System)
    - NTFS
        - Known as Journaling file system
        - In failure, they can automatically repair files/folder using information stored in log file

    - Advantages of NTFS over FAT
        - Support larger than 4GB
        - Set specific permission in files and folder
        - Encryption of file system


- **Windows System32 Folders**
    - System environment variable for window directory is
    ```
    %windir%
    ```
    - Environment variable store info about OS like
        - OS path
        - Number of processors used by OS
        - Location of temporary folders

- **User Accounts, Profiles and Permission**
    - Two types of account
        - Administrator 
        - Standard User
    - Check number of user
        - Startmenu
        - Other user(type)
    - Alternative to access it. Open run and type
    ```
    lusrmgr.msc
    ```

    - **User Account Control**
        - To protect user from high privilege misuse user account control is developed

    - **Settings and control panel**
        - Control panel access more complex settings and perform more complex actions


- **System Configuration**
    - System configuration utility(MSconfig) is for advanced troubleshooting
    
**What is the name of service that lists system Internals as the manufacturer?**
- psshutdown


- **Computer Management(compmgmt)**
    - It has three primary has three sections

- **System Information**
    - Microsoft system information(Msinfo32.exe) tool gather information about your system hardware, system components and software environment

- **Resource Monitor(resmon)**
    - It displays per process and aggregate CPU, memory, disk and network usage information

- **Registry Editor(regedit)**
    - It is for advanced computer users
    - To view or edit registry

-**Windows Update**
    - Updates are typically released on 2nd tuesday of each month called patch tuesday
    - But in case of emergency they push the update via window update service

- **Window Security**
    - It is your home to manage the tools that protect your device and your data

- **Bitlocker**
    - On device with Trusted Platform Module(TPM) installed, Bitlocker offers best protection
    - TPM is hardware component installed in many newer computers by computer manufactures

- We should use a removable drive on system without a TPM version 1.2 or later. What does this removable drive contain? - Startup key

- **Volume shadow copy Service**
    - To create a consistent shadow copy also known as snapshot or point-in-time copy of data that is to be backed up
    - Malware writer know this feature and write code in malware to look for these file and delete them doing this makes impossible to recover from ransomware attacks unless you have offline/offsite backup