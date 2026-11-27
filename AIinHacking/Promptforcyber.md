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

```
You are a security assistant for a Kali Linux lab.

Task: Produce a 3-step host recon plan for subnet 192.168.1.0/24

Constraints:
- Lab only, do not scan anything outside of 192.168.1.0/24.
- Keep commands safe and fast
- Step 1: Host discovery only
- Step 2: For one found host, identify top open ports quickly.
- Step 3: For that same host, grab lighweight version info for those ports.
- Avoid intrusive NSE scripts.

Output format(Exactly this markdown table):

|Step|Command|Why|Safe?(Yes/No)|
```



# Few shot prompt

```
You are a security assistant: I want a consistent, minimal incident note format.

Here is an example of the exact format to copy:

===Incident Note===
Title: SSH brute-force attempts
Scope: Lab VM only
Evidence:
-IP:192.168.1.5|Attempts:12
-IP:192.168.1.7|Attempts:5
Summary: Multiple failed SSH attempts observed against the VM.
Next Steps:
- Block offending IPs at lab firewall
- Rotate lab credentials
=========================
```

```
Now produce a New incident note in the same format for:
- Title: Suspicious HTTP traffic
- Scope: Lab VM only
- One sentence summary
- Two actionable Next steps
```

- If you have huge amount of log file
```
You are a SOC summarizer. Summarize the FAILED SSH login attempts in the text below.

Constraints:
- Ignore successful logins
- Group by source IP and show count of failures
- Output a 2-column markdown table with headers:IP|Failed_Attempts
- Then provide a one-line summary.

Text:
Aug 24 10:11:02 kali sshd[1234]: Failed password for invalid user admin from 192.168.1.5 port 49210 ssh2
Aug 24 10:11:05 kali sshd[1235]: Failed password for root from 192.168.1.5 port 49218 ssh2
Aug 24 10:12:10 kali sshd[1236]: Failed password for invalid user test from 192.168.1.7 port 51512 ssh2
Aug 24 10:12:35 kali sshd[1237]: Accepted password for kali from 192.168.1.10 port 52222 ssh2
Aug 24 10:13:01 kali sshd[1238]: Failed password for root from 192.168.1.5 port 49230 ssh2
```
      
- Safety rewrite of aggressive command: refacto risky nmap command into a safe version
```
You are a security assistant for a kali Linux lab.

Task: Review the following command and provide a safer, lab-scoped alternative with the same goal.

Aggressive command:
nmap -A -p- 192.168.1.0/24

Constraints:
- Lab only, do not scan outside 192.168.1.0/24
- Keep runtime reasonable(<5minutes)
- Reduce intrusiveness(no full -A scan over entire subnet)

Output:
1. Safer replacement commands in once code block
2. One-sentence rationale
3. One caution if applicable
```
 