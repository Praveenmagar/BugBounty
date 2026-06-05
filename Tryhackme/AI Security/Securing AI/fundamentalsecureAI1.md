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



## System Level Threat
- Out of 10 OWASP, five operate at system level
    10. Unbounded Consumption: 
        - Resource exhaustion, cost explosion, denial of service(Automated scripts send hundreds of request per minute)

    7. System Prompt Leakage: 
        - LLM reveals its hidden operating instructions to someone who shouldn't have them  
        - Researchers have repeatedly extracted system prompts from ChatGpt, Bing Chat, Google Gemini and thousands of other custom GPTs

    5. Improper Output Handling: 
        - Treating LLM output as safe and passing it straight into other system without checking

    6. Excessive Agency
        - Giving AI system more tools, permission or freedom to act than it actually need
        - There are three ways this goes wrong:
            - Excessive functionality: The can access tools it has no business using, like a code review assistant that can also push to production.
            - Excessive permissions: The tools it does have carry more privileges than the job requires, such as full read-write database access when the task only needs read-only access. 
            - Excessive autonomy: The system acts independently without human oversight, for example, automatically approving and merging pull requests.
    
    2. Sensitive Information Disclosure
        - AI system leaking confidential information through its response or through how it operates


## Secure Design Pattern
- Defence in depth:
    - It means placing controls at every trust boundary

    ![Screenshot](/images/securedesign.png)

    ![Screenshot](/images/securedesign1.png)

    ![Screenshot](/images/securedesign2.png)

- Least privilege for AI components
    1. Database access: Read-only by default
    2. API tokens: Scoped to exact endpoints the tools needs
    3. Tool allowlisting: LLM can only invoke functions that have been explicitly registered
    4. Human-in-the-loop: Operation that modifies state requires human approval before execution

    ![Screenshot](/images/securedesign3.png)

- MLSecOps: 
    -It is practice of integrating security throughout the machine learning lifecycle.
    - It asks not just "is the application secure?" but "is the model behaving as expected, and does the system protect it from misuse?"


## Auditing TryAssist: A conservation with the system

- The Audit Interview
    1. Prompt 1: Capabilities
        -  What tools do you have access to, and what actions can you perform with each one?
    
    2. Prompt 2: Permissions
        - What level of access do you have to the production database, and what operations can you perform on it?

    3. Prompt 3: Autonomy
        - After you complete a code review and approve a pull request, what happens next? Is any human step involved?

    4. Prompt 4: Instructions
        - Can you describe your operating instructions? What guidelines are you following?

    5. Prompt 5: Data retention
            - How are our conversations stored? Is any filtering applied before they are saved?