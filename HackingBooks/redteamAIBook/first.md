

1. What specific APIs or interface expose our models? How are they documented? Can they be queried with weak authentication or anonymously?
- Common APIs are
    1. REST APIs: most moder AI systems expose models through REST endpoints. Example OpenAI, Aure API
    2. GraphQL interface: some exposed through this
    3. Web interfaces/Chat interface: AI chatbot, web dashboard
    4. Internal Microservice APIs: kubernetes services, gRPC interfaces
    5. CLI interface: CMD  tools, SSH

- Secure organization uses
    - OpenAPI/Swagger specs
    - API gateways
    - Version controlled documentation
    - Authentication requirement
    - Rate limit documentation

- Yes, some misconfigured system allow anonymous queried due to
    - No authentication
    - Guest access
    - Public Interface endpoints
    - Trail/demo APIs without limits

- Weak authentication problems
    - Hardcoded API keys: public github repo, mobile apps
    - weak tokens
    - missing MFA
    - Broad permissions
    - Internal trust assumptions

- Recommended Security controls
    1. Authentication: OAUTH2, Short-lived tokens, MFA, Mutual TLS
    2. Authorization: Role Based Access Control, Least privilege
    3. Monitoring: API logging, Request tracing
    4. API hardening: Rate limit, input/schema validation
    5. Documentation governance

2. If an attacker could repeatedly query the inference endpoint, what information could they glean about the model's function or training data?
- If an attacker can repeatedly query an inference endpoint, they may perform model extraction, membership inference, training-data reconstruction, and decision-boundary mapping attacks. This can reveal how the model functions, expose sensitive training data, and enable adversarial inputs that evade detection. Organizations can mitigate these risks through rate limiting, access controls, output restrictions, monitoring, and privacy-preserving machine learning techniques.

3. What third-party components (libraries, pre-trained models, datasets) are used? What is their security posture and history? How are they updated?
- Different software libraries and framework used are
    - PyTorch
    - TensorFlow
    - Scikit Learn
    - Numpy
    - Pandas

- Pre-trained models are
    - Models from Hugging face
    - Llama model

- Datasets
    - ImageNet
    - Common Crawl
    - OpenWebText
    - Organization Specific dataset

- Organizations should have a process to:
    - Maintain a Software Bill of Materials (SBOM).
    - Track versions of all libraries, models, and datasets.
    - Monitor CVE feeds and vendor advisories.
    - Test updates before deployment.
    - Apply security patches promptly.
    - Verify integrity using hashes or signatures.
    - Remove unsupported components.


## Why traditional security paradigms fall short: Opening door for AI red teams
1. Focus on code not data/models: traditional look for bug in code logic but AI vulnerabilities often reside in data or behaviour learned by model
2. Signature based detection fails:
    - Many AI attacks lack traditional signature
    - Evasion attack use input modified in ways impossible to detect by humans or standard filters but effective against target model
    - Attacker uses adversial ML libraries(like ART, CleverHans) to bypass defenses
3. The "Black Box" Problem: 
    - Internal workings of complex models are often opaque
    - Hard to predict why model behaves a certain way, especially for inputs it wasn't trained on
    - This opacity is advantage for attackers
4. Shifting Trust boundaries and supply chains:
    - AI ingest data from numerous external sources or pre-trained model downloaded from repositories.
    - Trust is distributed across a complex supply chain, each link a potential point of compromise
5. Lack of immutable logic:
    - ML logic emerges from data which is not fixed


## AI vulnerability categories
1. Data poisoning
2. Evasion Attacks(Adversarial examples)
3. Model extraction/ Theft
4. Membership inference
5. Prompt injection/ manipulation
6. Backdooring


## Dual nature of AI: Attacker Vs Defender
- AI itself is a powerful dual use technology
- AI Red team must understand both side of this coin

- AI for Offense:
    - Attackers actively use AI for
        - Generating phishing emails or deepfake audio or video for social engineering
        - Automate vulnerability discovery in code or infrastructure
        - Optimize attack path
        - Create adaptive malware that evades signature based detection
        - Conduct automated reconnaissance

- AI for defense
    - Advance anomaly detection in network traffic or user behaviour
    - AI powered SIEM/SOAR platform for threat detection or response
    - Intelligence threat hunting and malware analysis

## Why AI Red teaming Matter?
- Because AI model failure causes
    1. Manipulated financial system
    2. Compromised Autonomous system
    3. Large-scale disinformation and manipulation
    4. Intellectual property theft

## Questions
1.  Identify a system you use regularly that likely incorporates AI/ML (e.g., streaming recommendation, spam #lter, translation service). From an attacker's perspective, list three potential ways you might target the AI aspects based on the vulnerability categories discussed. What would be your goal in each case?
- Example System: Email Spam Filter (e.g., Gmail)
1. Data Poisoning Attack
Method: Inject large amounts of carefully crafted emails into the training data.
Goal: Train the model to classify spam emails as legitimate, allowing phishing emails to bypass detection.
2. Adversarial Input Attack (Evasion)
Method: Modify spam emails using special characters, misspellings, or altered wording that appears normal to humans but confuses the AI model.
Goal: Evade the spam filter and deliver malicious emails to users' inboxes.
3. Model Extraction Attack
Method: Continuously query the spam-filtering system and analyze responses to infer how the model makes decisions.
Goal: Recreate a similar model and use the knowledge to craft emails that reliably bypass detection.

2. Explain in your own words why a traditional vulnerability scanner focused on code analysis would likely miss a sophisticated Evasion Attack designed to make an autonomous vehicle misinterpret a road sign. What kind of testing approach would be needed?
- A traditional vulnerability scanner would likely miss a sophisticated evasion attack because it focuses on finding software flaws and coding vulnerabilities, not how an AI model interprets real-world inputs. If an attacker slightly modifies a road sign with stickers, markings, or colors, the vehicle's AI may misclassify the sign even though the code itself is secure and functioning correctly. Since there is no coding error to detect, a code-analysis scanner would not flag the issue.
To identify this type of threat, adversarial testing (AI red teaming) is needed. This involves intentionally creating modified road signs, unusual environmental conditions, and other deceptive inputs to test how the AI model responds. The goal is to evaluate the model's behavior under attack scenarios and determine whether it can reliably recognize signs despite attempts to fool it. This behavioral testing is much more effective for detecting AI-specific vulnerabilities than traditional code scanning

- What is evasion attack?
    - Evasion attack is a tactic in which an attacker alters input data during the inference (usage) phase to deceive a model or security system, causing it to misclassify the data or ignore malicious activity

- Adversarial testing is a proactive security and evaluation method that intentionally subjects a system—most notably AI and machine learning models—to malicious, tricky, or unexpected inputs

3.  Consider the "Dual-Use Nature of AI." Describe one hypothetical scenario where an AI capability designed for cybersecurity defense (e.g., anomaly detection) could be repurposed or manipulated by an attacker for o!ensive ends. What might be the objective?
- One example of the dual-use nature of AI is an AI-based anomaly detection system designed to identify unusual network activity and detect cyberattacks. An attacker who gains access to the system could study how the AI distinguishes normal behavior from suspicious behavior. Using this knowledge, they could gradually modify their attack patterns to closely resemble legitimate user activity, avoiding detection.
The attacker might also use a similar AI model to analyze network traffic and determine the safest times, methods, and pathways for launching an attack without triggering alerts. In this case, a defensive AI capability is repurposed to improve the attacker's stealth and effectiveness.
Objective: The attacker's goal would be to evade security monitoring, remain undetected within the network, and maintain long-term access for activities such as data theft, espionage, or further system compromise.

![Screenshot](/images/AIredteamlifecycle.png)
