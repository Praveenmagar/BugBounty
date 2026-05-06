# Hacker PlayBook 3

## Penetration Testing Vs Red team
- Penetration Testing is the more rigorous and methodical testing of a network, application,hardware, etc
- Companies still need penetration testers to be a part of their secure software development life cycle (S-SDLC)
- Red teams are those who come up with same ideas and tatics as real attackers come.
- The Red Team’s mission is to emulate the tactics, techniques, and procedures (TTPs) by adversaries. 
- The goals are to give real world and hard facts on how a company will respond, find gaps within a security program, identify skill gaps within employees, and ultimately increase their security posture
- it is not as methodical as penetration tests

**We almost never run a vulnerability scan against the internal network because  are very loud on the network and will most likely get caught in today’s world**

 ![Screenshot](/images/redteamvspentest.png)

 - Two strong metrics that evolve from these campaigns are 
    1. Time To Detect (TTD) and 
    2. Time To Mitigate (TTM)

## What does Time To Detect mean?
- It is the time between the initial occurrence of the incident to when an analyst detects and starts working on the incident

## What does Time to Mitigate mean?
- It is the secondary metric to record. This timeline is recorded when the firewall block, DNS sinkhole, or network isolation is implemented.
- The other valuable information to record is how the Security Teams work with IT, how management handles a critical incident, and if employees panic

**With all this data, we can build real numbers on how much your company is at risk, or how likely it is to be compromised**

- As Red Teamers, our job is to test if the overall security program is working


#### Assumed breach exercise
- Since Red Team campaigns focus on detection/mitigation instead of vulnerabilities, we can do some more unique assessments.
- One assessment that provides customers/clients with immense benefit is called an assumed breach exercise where there will always be 0-days assumption. 