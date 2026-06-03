# AI forensics

## Digital Forensics and Incident Response(DFIR)
- It covers the collection of forensics artifacts from digital devices such as computer, media devices and smartphones to investigate an incident

## Why do we need DFIR?
1. Finding evidence of attacker activity
2. Robustly removing the attacker
3. Identifying extent and timeframe of breach
4. Finding loophole that led to breach
5. Understanding attacker behaviour to block future intrusion attack
6. Sharing information about attacker within community

- Digital forensics and Incident Response are highly interdependent
- Incident response leverages knowledge gain from digital forensics and digital forensics take its goal and scope from incident response process

## Basic concept of DFIR
- Artifacts:
    - They are pieces of evidence that point to an activity performed on a system
    - E.g to clain attacker used Window registry key to maintain persistence on a system, we can use said registry key to support our claim

- Evidence Preservation
    - First: Evidence is collected and make write protected
    - Second: copy of write protected is used for analysis

- Chain of Custody
    - After collecting evidence, it must be kept in secure custody to maintain integrity
    - Any person not related to investigation must not process evidence

- Order of Volatility
    - It is important to understand order of volatility of different evidence sources
    - E.g Between RAM and hard drive, We need to preserve RAM before preserving hard drive

- Timeline Creation
        - It provides perspective to investigation and helps collate information from various sources to create story of how things happened

## DFIR Tools
1. Eric Zimmerman's tools
2. Kroll Artifact Parser and Extractor(KAPE)
3. Autopsy
4. Volatility
5. Redline
6. Velociraptor


## Incident Response Process
- In Security Operations, the prominent use of Digital Forensics is to perform Incident response
- Different organization have published standardized method to perform Incident response. Some of them are
1. NIST step
    - Preparation
    - Detection and Analysis
    - Containment, Eradication and Recovery
    - Post-Incident Activity

2. SANS steps
    - Preparation
    - Identification
    - Containment
    - Eradication
    - Recovery
    - Lessons Learned

## AI forensics Landscape

![Screenshot](/images/aiforensics.png)

## AI Limitation
1. Probabilistic Vs Deterministic
    - Traditional softwarea and algorithms are deterministic, same input same output
    - Today AI and modern machine learning models are probabilistic, they use statistical model to learn from data and make predictions with certain possibilities
    - But digital forensics field demands consistent and repeatable result

2. Accuracy vs Precision vs Recall
    - Accurcay: 
        - if there are 100 files, 99 are benign(harmless) and, one is malicious.
        - If a model were to predict all files to be benign, it would achieve 99% accuracy, but this does not make it efficient. Overfitting, where a model can be overtrained on , can directly affect the accuracy of a model.
    - Precision:
        - Higher precision = fewer false positive
        -  in isolation as the model can choose to be very selective, only flagging the very obvious malicious files, meaning some malicious files may be missed
    - Recall
        - Recall measures how successful the model was in identifying all positives in the provided dataset


## AI & DFIR
- Four key areas of DFIR
    1. Image and video forensics
        - Convolutional Neural Network(CNN): It automatically learns patterns in data using small filter commonly used for images
        - Examples
            - CNN based forgery detection: Researcher started combining traditional forensics like Error level analysis(ELA: technique used in image forensics to detect areas of image that may been digitally altered) with CNN to identify image tampering with accuracy rating 94%
            - Deepfake detection: best way to tackle attacker using AI is by controlling and using it by ourselves. CNN models have recently started being used in conjunction with some other AI technologies to develop specialised detectors.
            - Generative Adversarial Networks(GANs):It is one of exciting development in image and video forensics, a setup where two neural network compete: one generates fake video and other tries to detect it
    
    2. Communication Analysis
        - It involves processing and analysis of large volume of text
        - Phishing Email detection
            - Transformer based model trained for Natural language processing like BERT and RoBERTa, excel at identifying phishing email with 99% accuracy
        - Chat log and Social media analysis
            - Same above technique is used to automatically scan chats for keywords or pattern related to threats

    3. Timeline reconstruction and user behaviour
        - It is common and critical part of investigation, with labour intensive and time consuming task.
        - ML help us in
            - Automated event timeline reconstruction
            - Anomaly detection
    4. Malware detection/analysis
        - Deep neural network made possible to classify file as malicious or benign(e.g microsoft and intel's stamina project)
        - ML is use for dynamic analysis to detect malicious or not
        - AI/ML is very common in antivirus and endpoint detection response product


## AI ethical and legal Implications
- Key components we need to consider when using AI in DFIR
    1. Explainability and tranparency
    2. Bias and fairness
    3. Accountability and chain of custody
    4. Privacy and data protection
    



## Digital Trail Practical
- Lets start Investigation
    - Activate Virtual environment
    - As forensic investigator, isolation is key
    - In virtual env, any tool you run or changes don't contaminate original evidence
        ```
        source /opt/dfir-env/bin/activate
        ```
        - It activates dfir-env
    - Here, we use classify_logs.py made by one of investigator engineer
    - It uses an AI model trained on labelled log data to understand what "normal" logs look like and spot potentially suspicious anomalies
    - lets runs this against auth.log to find any suspicious
        ```
        python3 /opt/dfir-lab/classify_logs.py /var/log/auth.log
        ```
        - Outpur of this show few log line have been identified as suspicious
    - Let's use another model trained on certain high priority directories and their contents like filename, path, size, extension, entropy, permission, and creation time to identify petentially suspicious file
        ```
        python3 /opt/dfir-lab/file_anomalies.py
        ```

    - Constructing the Timeline
        - Now, use our human insight to validate the findings of the ML script and see if they can shed any light on whether an attack has taken place, and how.
        - Phase 1: Initial Access
            - The first key artefact the ML script flagged for us is
                ```
                /tmp/invoice_dump.txt
                ```
            - By listing its contents, we find it is kind of data dump
            - One important info is invoice_Q1_2075.ods contained within /Documents/Invoices/
            - We don't know its home directory, but if we combine with suspicious auth.log files flagged earlier, then it shows first user account to access was j.morgan, the best place to look next is /home/j.morgan/Documents/Invoices/
                ```
                cat /home/j.morgan/Documents/Invoices/invoice_Q1_2075.ods
                ```
            - It is very malicious showing attack start with phishing email
            - Check email
            - After checking email confirms our suspicions and now we reconstruct how attacker gained initial access
                1. Phishing email sent to j.morgan
                2. malicious .ods file opened, triggering data harvesting
                3. Data saved to /tmp/invoice_dump.txt and exfiltrated to the attacker
                4. Attacker logs into j.morgan using collected or replayed credentials
                5. Access escalates from there

        - Phase 2: Tooling and Infrastructure
            - Attacker used harvested information like usernames, shell history, and SSH configuration to log in as j.morgan
            - After that, they deployed additional tooling to enable remote access
                ```
                cat /tmp/.syncd
                ```
                - connects to http://attacker_ip/payload.sh and executes it
                ```
                cat /tmp/.x
                ```
                - Establishes remote shell to attacker_ip:4444
        
        - Phase 3: Privilege Escalation
            - Next big question: How did attacker move from j.morgan to highly privileged r.house
                1. After accessing j.morgan account they found j.morgan could run certain commands with sudo privileges
                2. Using sudo they open
                    ```
                    sudo /home/r.house/.ssh/authorized_keys
                    ```
                3. Attacker added own SSH public key to that file
                4. After adding key, they could SSH directly into the r.house account without knowing its password

        - Phase 4: Disguise and Persistence
            - Now operating as r.house, the attacker was in high privileged position

            ![Screenshot](/images/privilegeesalate.png)

            - The key idea is that the attacker hid a reverse shell inside a file that looked like a normal system monitoring tool (sysmon) and created supporting log files (boot_monitor.log) to make it appear legitimate, allowing them to regain access later without repeating the original compromise

        - Phase 5: Source code Theft
            - Now, attacker had gained privileged access and persisted, but what was their ultimate objective?
            - Here, source code was stolen, as well as their OS and boot loader
