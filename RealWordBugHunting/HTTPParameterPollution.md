# HTTP Parameter Pollution (HPP)
- It is process of manipulating how a website treats a parameter it receives during HTTP request
- Two types
    - Server Side HPP
    - Client Side HPP

**Server Side HPP**
- Normal URL
``` text
https://wwww.bank.com/transfer?from=12345&to=6789&amount=5000
```
- Polluted URL
``` text
https://www.bank.com/transfer?from=12345&to=6789&amount=5000&from=ABCDE
```
**Here**
- PHP and Apache use last occurrence
- Apache tomcat uses first occurrence
- ASP and IIS uses all occurrences

**Hidden server-side Behaviour**
- Not included form parameter in the URL
- Normal URL
```text
https://www.bank.com/transfer?to=6789&amount=5000
```
- Polluted URL
```text
https://www.bank.com/transfer?to=6789&amount=5000&from=ABCDE
```

**Example**

**Hackerone Social Sharing Buttons**
- To find HPP vulnerability look for link that appears to contact other services
- Normal URL
 ```text
https://hackerone.com/blog/introducing-signal
```
- Polluted URL
```text
https://www.facebook.com/sharer.php?u=https://hackerone.com/blog/introducing-signal?&u=https://vk.com/durov
```

**Twitter Unscribe Notification**
- Normal URL
```text
https://twitter.com/i/u?iid=F6542&uid=1134885524&nid=22+26&sig=647192e86ef-------
```
- Polluted URL
```text
https://twitter.com/i/u?iid=F6542&uid=2321301342&uid=1134885524&nid=22+26&sig=647192e86ef-------
```

# Summary
- HPP vulnerability require more testing than some other vulnerabilities
- Social media links are good place to search for HPP first