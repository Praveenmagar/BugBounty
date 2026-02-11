# Finding secret using shodan
- **Internet VS WWW**
    - WWW is one of the various services offered by internet in order to share information
- **Google**
    - Search engine crawl WWW
- **Shodan**
    - Ethical hacker's search engine crawl Internet
- **Shodan is the world's first search engine for internet connected devices**

## Shodan
- **Log into shodan**
- search into shodan
```text
webcam
```
```text
country:"India" webcam
```
```text
port:21
```
```text
asn:as32934
```
-**For more deeper**
```text
asn:as32934 http.title:"5xx Server Error"
```
- **To remove something use hyphen(-) symbol
```text
asn:as32934 -http.title:"Error" -http.title:"5xx Server Error"
```

- **For facebook meta certificate**
```text
ssl:"Meta Platforms, inc."
```