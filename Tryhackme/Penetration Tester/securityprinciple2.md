# Principles of Security

- CIA traid

- Two key concepts are used to assign and manage the access rights of individuals:
    - Privileged Identity Management (PIM)
    - Privileged Access Management (PAM).

**If you wanted to manage the privileges a system access role had, what methodology would you use?**
- PAM

**If you wanted to create a system role that is based on a users role/responsibilities with an organisation, what methodology is this?**
- PIM

## Some popular and effective security models used to achieve the three elements of the CIA triad
- The Bell-La Padula Model
    - Used to achieve confidentiality

        ![Screenshot](/images/belllapadula.png)

- Biba Model
    -  Arguably the equivalent of the Bell-La Padula model but for the integrity of the CIA triad
    -  It is used in organisations or situations where integrity is more important than confidentiality

        ![Screenshot](/images/bibamodel.png)



## Threat modeling and incident response
- Threat modelling is the process of reviewing, improving, and testing the security protocols in place in an organisation's information technology infrastructure and services.
- A critical stage of the threat modelling process is identifying likely threats that an application or system may face, the vulnerabilities a system or application may be vulnerable to.
- It is similar to a risk assessment made in workplaces for employees and customers. The principles all return to:
    - Preparation
    - Identification
    - Mitigations
    - Review

- Complex process that needs constant review and discussion with a dedicated team need effective threat model 
    - Threat intelligence
    - Asset identification
    - Mitigation capabilities
    - Risk assessment

- Frameworks used
    - Spoofing identity, Tampering with data, Repudiation threats, Information disclosure, Denial of Service and Elevation of privileges(STRIDE)
    - Process for Attack Simulation and Threat Analysis(PASTA)

    - STRIDE

        ![Screenshot](/images/stride.png)


- Incident
    - A breach of security is known as an incident.
    - Despite all rigorous threat models and secure system designs, incidents do happen.
    - Actions taken to resolve and remediate the threat are known as Incident Response (IR)

        ![Screenshot](/images/incident.png)

    - Incident is responded to by a Computer Security Incident Response Team(CSIRT)
    - Six phases to solve incident

        ![Screenshot](/images/incidnet.png)
