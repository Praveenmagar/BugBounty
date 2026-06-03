# ContAInment

## To identify ransomeware threat with the help of AI. Your job is to investigate the incident: identify how the attacker gained access, trace their actions, recover any stolen data, and neutralise the threat

1. At first open victim machine with the help of SSH
    - Company provide ssh with its password. Now open terminal and put following
        ```
        ssh o.deer@10.49.139.212
        ```
        - They will ask for password and put password now you will get victim terminal

2. After getting access try to find out details by listing its content and check each directory
    - Here in download i get one invoice_payload.scr. Now i want to copy it to my terminal
        ```
        scp o.deer@10.49.139.212://home/o.deer/Downloads/invoice_payload.scr .
        ```
    - After doing this they will ask for ssh password put that then invoice_payload.scr is copied to my attacker machine. Dont forget to put dot(.) at last

3. We have mail folder as well in victim directory
    - Now lets us AI model to scan mail folder
        ```
        can you search files in this directory /home/o.deer/Mail for phishing email
        ```
    - Whatever suspected you find just copy it to your own terminal for later investigation
        ```
         scp o.deer@10.49.139.212://home/o.deer/Mail/2025-06-17_invoice_required_review.eml .
        ```
    - Lets copy another as well
        ```
        scp o.deer@10.49.139.212://home/o.deer/westtech_projects_encrypted.zip .
        ```

4. Lets use email extractor to check email file
    ```
    eml-extractor -f 2025-06-17_invoice_required_review.eml
    ```
- We get nothing at all

5. Inside documents we found pcap file and our AI model suggest that 17 june mail is suspected to be phishing email. 
    - Now let's copy 17 date pcap file to check as well in our terminal
    - Create one pcap folder
        ```
        mkdir pcap
        ``
    - Copy all contents of 17 using *
        ```
        scp o.deer@10.49.139.212://home/o.deer/Documents/pcap_dumps/2025-06-17/* pcap/
        ```
    - Check the pcap file all file are almost of same size but one is bigger that another. Now lets use AI model to scan it
        ```
        reassemble pcap file session_4444_dump.pcap in the directory /home/o.deer/Documents/pcap_dumps/2025-06-17
        ```
    - We have different pcap file in 2025-06-17. Now let's merge all in one place
        ```
        mergecap * -w AI.pcap
        ```
        - Now open AI.pcap using wireshark
            - After opening, go to value and right click and go to follow and TCP stream and you will get details there
            - Lets copy key given there: " **w#e@%s~t^t-e$c*h_v^i%ct_im_1**"

    - Here, the upper AI model has complete scan and the PCAP file has been successfully reassembled and cleaned, outputting to:
        ```
        /home/o.deer/qwen-output/reassembled_data_dump.txt
        ```
        - You can go and use cat to view it and you will get there key
        - Now use that key to unzip westtech_projects_encrypted.zip file
        - After unzip we see one directory with thm_flags.txt
        - Use nano to open that directory
        - Now go to /home/o.deer/westtech_project and list, there is one thm_flag_guide.txt
        - cat it to see about flag. Now here it is saying flag is base 64 encoded. So let's go to cyberchef to decode it
        - It's little difficult to find the flag directly. So lets use AI model for this work
            ```
            flag file /home/o.deer/home/o.deer/westtech_projects/thm_flags.txt
            ```




