# 🐞 Bug Bounty Notes (Quick Reference)

## 🔎 Shodan Dorks
```text
http.title:"WordPress" "WordPress 4.9" OR "WordPress 5.7" OR "WordPress 5.8"
```

```text
Server:Prismview Player
```

> Used to identify exposed WordPress installations and misconfigured digital billboards/media players.

---

## 📘 Important Terms

- **Vulnerability**  
  Weakness in a system.

- **Exploit**  
  Technique used to abuse a vulnerability.

- **Payload**  
  Malicious code delivered through an exploit.

### 🧪 Example
- PDF file containing a reverse shell  
  - PDF file → **Exploit**  
  - Reverse shell → **Payload**

---

## 🌐 HTTP Request Components

- **HTTP/1.1**  
  Communication protocol version.

- **Cookie**  
  Used for user identification and session tracking.

- **Cache-Control: max-age=0**  
  Tells browser not to cache the response.

- **User-Agent (UA)**  
  Identifies browser, OS, and device.

---

## 🤖 Bug Bounty Automation Tools

- **Nucleifuzzer** – Automated vulnerability fuzzing  
- **Reconflow** – Best for wide scope targets  
- **MagicRecon** – Best for narrow/single scope targets  
- **Custom Bash Scripts** – Fully controlled automation

---

## ⚙️ How to Run Automation

- **Single domain (abc.com)**  
  - Use MagicRecon  
  - Combine with Nucleifuzzer

- ⚠️ Do not rely only on automation  
  - Manual testing is critical  
  - Automation finds only low-hanging issues

---

## 🌍 Target Scope Types

- **Single Domain**
```text
abc.com
```

- **Wildcard Domain**
```text
*.abc.com
```
Includes all subdomains such as api, admin, dev, etc.

---

## ✅ Key Takeaway
Automation helps, but real bugs come from logic, manual testing, and curiosity.
