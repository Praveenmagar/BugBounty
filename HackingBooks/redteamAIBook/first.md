

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

    34 page