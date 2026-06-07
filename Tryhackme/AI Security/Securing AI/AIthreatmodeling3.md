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