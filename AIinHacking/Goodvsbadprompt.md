# Good vs Bad Prompt

## Bad Prompt
```
Give me an nmap command for a network
```

## Good Prompt
```
You are a security assistant for a Kali Linux lab.

Tasks: Propose one safe host-discovery command to find live hosts on subnet 192.168.1.0/24.

Constraints:
- Lab only, do not scan outside of 192.168.1.0/24
- Runtime < 3 minutes on a laptop
- Be conservative with flags(no intrusive scripts or flags).
- Explain flags in one sentence

Output format:
- A single code block with the command.
- Then one sentence explaining why these flags are safe in a lab.
```