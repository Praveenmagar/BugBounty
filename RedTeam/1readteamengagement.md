# How to have successful engagement?
- The key to successful engagement is well coordinated planning and communication through all parties involved

# How this engagement occurs in Red team?
- Tabletop exercise
- Adversary emulation
- Physical assessment

- **How engagement are categorized?**
    - Focused adversary emulation
        - define a specific APT or group to emulate within an engagement i.e.finance institutions and APT38
    - General internal/network penetration test
        - test will follow a similar structure but will often be less focused and use more standard TTPs(Tactics, Techniques, and Procedures)

- **Engagement require well define scope like following**
    - No exfiltration of data.
    - Production servers are off-limits.
    - 10.0.3.8/18 is out of scope.
    - 10.0.0.8/20 is in scope.
    - System downtime is not permitted under any circumstances.
    - Exfiltration of PII is prohibited.

- **Rules of Engagement**
    - First "official" document in the engagement planning process and requires proper authorization between the client and the red team. 
    - This document often acts as the general contract between the two parties; an external contract or other NDAs (Non-Disclosure Agreement) can also be used.

- **Engagement documentation**
- It includes following plan
    - Engagement plan
        - CONOPS(Concept of Operation): Non-technical overview of how red team meet client objective and target the client
        - Resource plan
    - Operations plan
        - Personnel: information on employee requirements
        - Stopping conditions
        - ROE(optional)
        - Technical requirement
    - Mission Plan
        - Command playbooks(optional): Exact command and tools to run, including when, why, and how
        - Execution time
        - Responsibility/roles
    - Remediation plan
        - Report
        - Remediation/Consultation

    - **CONOPS**
        - It should include the following in summary form
            - Client Name
            - Service Provider
            - Timeframe
            - General Objectives/Phases
            - Other Training Objectives (Exfiltration)
            - High-Level Tools/Techniques planned to be used
            - Threat group to emulate (if any)

    - **Resource Plan**
        - It should be written as bulleted lists of subsections
            - Header
                - Personnel writing
                - Dates
                - Customer

            - Engagement Dates
                - Reconnaissance Dates
                - Initial Compromise Dates
                - Post-Exploitation and Persistence Dates
                - Misc. Dates

            - Knowledge Required (optional)
                - Reconnaissance
                - Initial Compromise
                - Post-Exploitation

            - Resource Requirements
                -  Personnel
                - Hardware
                - Cloud
                - Misc

    - **Operational Plan**
        -  There is no standard set of operation plan templates or documents,below is an outline of example subsections within the operations plan.
            - Header
                - Personnel writing
                - Dates
                - Customer
            - Halting/stopping conditions (can be placed in ROE depending on depth)
            - Required/assigned personnel
            - Specific TTPs and attacks planned
            - Communications plan
            - Rules of Engagement (optional)


    - **Mission Plan**
        - Minimum detail should be include with this plan are
            - Objectives
            - Operators
            - Exploits/Attacks
            - Targets (users/machines/objectives)
            - Execution plan variations
