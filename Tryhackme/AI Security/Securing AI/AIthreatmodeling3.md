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


## Specific AI assets and Attack Surface

![Screenshot](/images/aiassets.png)

- A stolen database is serious, but a stolen model is a fundamentally different kind of loss, you can't just rotate a credential and move on

## Data supply chain and STRIDE's Gaps
- Knowing what to protect is only half the picture, we also need to understand how those assets are built, moved, and consumed, because every step in that process is an opportunity for compromise
- AI data supply chain

![Screenshot](/images/aisupplychain.png)


## Adapting STRIDE for AI System
1. S- Spoofing: Data Source Impersonation
    - In RAG(Retrieval-Augmented Generation) architecture, model retrieves context from external sources, vector databases, document stores, and web content and treats that context as trustworthy
    - An attacker who can inject content into these sources effectively spoofs the knowledge the model relies, causing it to generate attacker controlled information

2. T-Tampering: Data Poisoning
    - Attacker injects malicious data into training pipeline, causing the model to learn incorrect patterns

3. R- Repudiation: Unexplainable Model Decisions
    - Lack of Decision Audit Trails: When AI model makes a consequential decision, approves a loan, flags a transaction, or denies a claim, can you trace why? Most ML models lack built-in explainability.
    - Without robust logging of inputs, outputs, model versions, and retrieval context, reproducing or explaining a specific decision after the fact is extremely difficult

4. I- Information Disclosure: Model Extraction
    - An attacker systematically queries a model's API and uses the input-output pairs to reconstruct a functionally equivalent copy of the model. This requires no access to the model's internals, only its public facing endpoint is needed. The stolen model represents significant intellectual property loss and can be probed offline for adversarial weakness

5. D- Denail of Service: Inference Cot Exploitation
    - AI inference is orders of magnitude more expensive than traditional API calls. 
    - In cloud based deployments billed per token or per query, an attacker can inflict financial damage without taking the system offline. By generating large volumes of expensive queries, long prompts, requests for maximum-length outputs, they drive operational costs to unsustainable levels

6. E- Elevation of Privilege: Jailbreaking and Excessive Agency
    - An attacker crafts prompts that cause an LLM to ignore its safety guidelines, content policies, or behavioural restrictions.
    - The model is designed to refuse certain requests, but the attacker's input "elevates" their access to capabilities the model was instructed to restrict

## What STRIDE still misses
- Some AI threats don't map cleanly to any single STRIDE category
    - Adversarial examples: inputs designed to cause misclassification, span Tampering, Spoofing, and Elevation of Privilege depending on context. There's no single STRIDE lens that captures them fully.

    - Model bias and fairness issues are security-adjacent concerns with real regulatory and compliance implications, but they don't fit traditional threat categories. A biased model isn't being "attacked", it's failing in a way STRIDE wasn't designed to describe.

    - Emergent behaviours in large models, capabilities or behaviours that weren't explicitly trained for and may not be anticipated, are a class of risk with no traditional parallel. You can't threat model behaviour that nobody predicted would exist.

![Screenshot](/images/strideai.png)

## MITRE ATLAS: The AI Threat Technique Catalogue
- MITRE maintains it with contributions from industry, academia, and government

![Screenshot](/images/atlas.png)

- Key techniques you need to know
    1. Data Poisoning(AML.T0020): 
        - Injecting malicious data into training pipelines to corrupt model behaviour
        - Similar to STRIDE: Tampering
    2. Model Extraction(AML.T0024):
        - Systematically querying a model's API to reconstruct a functional copy.
        - Requires no internal access, just the public endpoint and enough queries
        - Similar to STRIDE: Information Disclosure
    3. Evade ML model(AML.T0015):
        - Crafting adversarial data that prevents a model from correctly identifying the contents of the input
        - Adversaries may use this to evade malware detection, bypass content filters
        - Similar to multiple STRIDE categories: Tampering, Spoofing, and Elevation of Privilege
    4. LLM Prompt Injection:
        - Manipulating an LLM's behaviour by injecting instructions through direct user input or indirect content the model processes
        - Similar to STRIDE: Tampering
    5. Backdoor ML model:
        - Embedding hidden triggers in a model during training

- Using ATLAS during Threat Modeling
    - ATLAS isn't a replacement for STRIDE, it's the enrichment layer. 
    - Two working together
        - Stard with STRIDE: Walk each AI component through the six threat categories to identify "What could go wrong"
        - Enrich with ATLAS: For each identified threat, look up the corresponding ATLAS technique to get the specific how, including documented attack methods and real world case studies
        - Apply mitigations: ATLAS provides recommended countermeasures for each technique, giving you actionable defensive guidance


## OWASP LLM Top 10: Mapping Risks to components

![Screenshot](/images/owasp.png)

- Component Risk Profiles
    - Risk profiles for the three most critical components
    1. LLM Inference Endpoint:
        - Carries the highest risk concentration
        - Appears in seven of ten OWASP entries: prompt injection, sensitive info disclosure, improper output handling, excessive agency, system prompt leakage, misinformation, unbounded consumption
        - This component requires most comprehensive hardening
    2. Vector Database/ RAG Pipeline:
        - Appears in three entries: indirect prompt injection via retrieved content, embedding weakness, misinformation
        - Hardening focuses on input validation for indexed content, access controls on the vector store
    3. Training Pipeline:
        - Primary component for data and model supply chain threats
        - Appears in three entries: sensitive data entering training, supply chain, data and model poisoning

![Screenshot](/images/awaspstride.png)

- STRIDE gives you the wide-angle view. ATLAS gives you the technical detail. OWASP tells you where to point the camera

## Practical

![Screenshot](/images/3lab1a.png)

![Screenshot](/images/3lab1b.png)

![Screenshot](/images/3lab1c.png)

![Screenshot](/images/3lab1d.png)

![Screenshot](/images/3lab1e.png)

![Screenshot](/images/3lab1f.png)