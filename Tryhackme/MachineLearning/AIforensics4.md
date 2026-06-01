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