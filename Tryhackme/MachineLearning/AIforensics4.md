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

