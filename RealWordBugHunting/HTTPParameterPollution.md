# HTTP Parameter Pollution (HPP)
- It is process of manipulating how a website treats a parameter it receives during HTTP request
- Two types
    - Server Side HPP
    - Client Side HPP

**Server Side HPP**
- Simple URL
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
- Simple URL
```text
https://www.bank.com/transfer?to=6789&amount=5000
```
- Polluted URL
```text
https://www.bank.com/transfer?to=6789&amount=5000&from=ABCDE
```

**Example**
-  *Hackerone Social Sharing Buttons*