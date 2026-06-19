# Prompt defense

## Probabilistic security
- Refusals aren't hard rules the model is force to follow, they're just patterns it learned to prefer during training
- There is no condition to bypass, no CVE to assign, no binary wall to knock down
- **Prompt injection cannot be fully solved within existing architectures, only mitigated**

- The System Prompt Isn't a wall
    - A natural response to what you've seen is to write a better system prompt, something longer, more explicit, and harder to override
    - A carefully constructed user input, a fake injected dialogue, or content pull in from an external source can effectively outweigh the system prompt, not by circumventing it technically, but by making compliance statistically more likely in that moment

- Defence in Depth
    - If no single control is reliable, the answer is to stack multiple controls so that breaking one still leaves an attacker facing others. This is defence-in-depth
    - No single defence can reliably stop all attacks, defence-in-depth is the only practical approach

    - Adding one layer to picture
        1. System prompt hardening: raising the bar at the instruction level
        2. Input guardrails: Catching malicious instructions before they reach the model
        3. Deployment controls: Limiting what a compromise model can actually do
        4. Output validation: Treating model output as untrusted before it touches downstream system
- **We tackle prompt vulnerabilities, not by closing the problem completely, but by making the attacker's job significantly harder.**