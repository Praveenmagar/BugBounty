# AI Threat Modeling

- In AI system,
    - Training data can be poisoned
    - Model weights can be stolen
    - Prompts can be injected
    - Being non-deterministic, same system can produce different output each time it's queried

## Web application Security
- Web application is like a program that we can use without installation as long as we have modern browsers like Firefox, Safari, or Chrome
- In web app program run on a remote server

![Screenshot](/images/webappsec.png)

## Categories of common attack against web app
1. Log in at the website: Attacker try to discover the password
2. Search for the product: attacker can attempt to breach the system by adding specific characters and codes to search term
3. Provide payment details: Attacker would check if the payment details are sent in cleartext or using weak encryption

## Threat Modelling
- It is a systematic approach to identifying, prioritising, and addressing potential security threats across the organisation

- Threat:
    - It is a potential occurrence, event, or actor that may exploit vulnerabilities to compromise information  confidentiality, integrity, or availability
    - It can come in various form like cyber attacks, human error, or natural disasters

- Vulnerability:
    - Weakness or flaw in a system that may be exploit by a threat to cause harm
    - It may arise from software bugs, misconfigurations, or design flaw

- Risk:
    - Possibility of being compromised because of threat taking advantage of a vulnerability

## High level process of threat modelling
1. Defining the scope
2. Asset identification
3. Identify threats
4. Analyse vulnerabilities and prioritise risks
5. Develop and implement countermeasures
6. Monitor and Evaluate

![Screenshot](/images/thteams.png)

## Attack Tree
- It is a graphical representation used in threat modelling to systematically describe and analyse potential threats against a system, application or infrastructure

## Threat modeling Framework
1. MITRE ATT&CK Framework
2. DREAD Framework
3. STRIDE Framework
4. PASTA Framework

## MITRE ATT&CK Framework
- MITRE ATT&CK(Adversial Tactics, Techniques, and Common Knowledge) is a comprehensive, globally accessible knowledge base of cyber adversary behaviour and tactics developed by MITRE corporation
- It is organised into a matrix that covers
    - Tactics: High level objectives
    - Techniques: methods used to achieve goals
- The framework includes descriptions, examples, and mitigatios for each technique
- Each techniques contains five significant sections
    1. Technique Name and Details
    2. Procedural Examples
    3. Mitigations
    4. Detections
    5. References

- Aside from incorporating MITRE ATT&CK in threat modelling process, it can be used in various cases depending on your organisation's needs
    1. Identifying potential attack paths based on your infrastructure
    2. Developing threat scenarios
    3. Prioritising vulnerability remediation


## Mapping with ATT&CK Navigator
- Steps and features we will use are
1. Creation of new layer
2. Searching and selecting techniques
3. Viewing, sorting and filtering layers
4. Annotating techniques with fills, scores and comments

## Creation of new layer
- When creating new layer there are three MITRE ATT&CK matrices
    1. Enterprise- used against enterprise network
    2. Mobile- Focuses on threats and techniques against mobile devices
    3. ICS- Focuses on threats and techniques against industrial control systems like power plants, water treatment facilities and transportation system

## Searching and selecting Techniques
- Use search function under Selection Controls panel


## DREAD Framework
- It is a risk assessment model developed by Microsoft to evaluate and prioritise security threats and vulnerabilities
- DREAD Stands for 
    - Damage: How bad would an attack be?
    - Reproducibility: How easy is it to reproduce the attack
    - Exploitability: How much work is it to launch the attack?
    - Affected Users: How many people will be impacted?
    - Discoverability: How easy is it to discover the vulnerability?

    ![Screenshot](/images/dread.png)

    ![Screenshot](/images/dread1.png)

## STRIDE FRAMEWORK
- Threat modelling methodology also developed by Microsoft

![Screenshot](/images/stride1.png)

![Screenshot](/images/stride2.png)

- Threat modelling with STRIDE
    1. System Decomposition
    2. Apply STRIDE categories
    3. Threat Assessment
    4. Develop Countermeasures
    5. Validation and Verification
    6. Continuous Improvement

## PASTA Framework
- PASTA(Process for Attack Simulation and Threat Analysis) is structured, risk-centric threat modelling framework designed to help organisations identify and evaluate security threats
- Seven step methodology

![Screenshot](/images/pasta.svg)
