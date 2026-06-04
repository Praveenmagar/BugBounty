# Securing AI System

## Anatomy of an AI system
- From traditional to AI- augmented
    - In traditional: Request flow from UI to API to database and back, and security teams know exactly where to place control
    - In AI model: new component appears, and data flows through paths that existing security controls were never designed to monitor

    ![Screenshot](/images/aisecurity.png)

- The TryAssist Architecture
    - It has nine components

    ![Screenshot](/images/tryassist.png)

    ![Screenshot](/images/aisecurity1.png)


![Screenshot](/images/trustboundary.png)

![Screenshot](/images/dataflow.png)


## OWSAP top 10 2025
1. Prompt Injection
2. Sensitive data disclosure
3. Supply chain
4. Data and Model Poisoning
5. Improper output validation
6. Excessive Agency: AI component with more privilege
7. System prompt leakage
8. Vector and Embedding weakness
9. Misinformation
10. Unbounded consumption

## MITRE ATLAS(Adversial Threat Landscape for AI System)
- It is knowledge base of adversary tactics, techniques, and case studies for AI system
- OWSAP classifies what vulnerabilities are
- ATLAS document how adversaries exploit them


## NIST AI Risk Management Framework(RMF)
- It approaches problem from an organisational perspective
- It's four functions describe how an organisation manage AI risk systematically
    1. Govern: Setting policies and accountability structure
    2. MAP: Identify AI system and their risk context
    3. Measure: Access and monitor risk level
    4. Manage: responding to and mitigating identified risk
    