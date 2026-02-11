# Live Recon- Gathering Everything
**For given site**
```text
app.admin.blog.example.com
```
- **com**
    - Top level domain
- **example**
    - root domain
- **blog**
    - first level subdomain
- **admin**
    - Second level subdomain
- **app**
    - Third level subdomain

## Classless Inter-Domain Routing(CIDR)
- It is an IP address allocation method that improves data routing efficiency on the internet
- Each machine, server and end-user device that connects to internet has a unique number called IP address
- Devices find and communicate with one another by using this IP addresses
- Organizations uses CIDR to allocate IP addresses flexibly and efficiently in their networks

## Autonomous System Number(ASN)
- It is a way to represent a collection of IPs and who owns them
- The IP address pool is spread across five regional internet registers(RIRs)
    - AFRINIC
    - APNIC
    - ARIN
    - LACNIC
    - RIPE NCC


**Note: Small organizations don't have dedicated CIDR range**

## Vertical VS Horizontal Correlation
- **If we take facebook as host then**
    - **Horizontal**
        - facebook.cn 
        - facebook.ir
        - instagram.com
        - whatapps.com
    
    - **Vertical**
        - blog.facebook.com
        - help.facebook.com
        - a.blog.facebook.com

# If facebook.com is target then perform following
- **Horizontal subdomain**
- **Vertical subdomain**
- **IP blocks**
- **Acquisitions**

## How to find IP blocks?
- **first way**
    - Go to this site
```text
 https://whois.arin.net/ui/ 
 ```
- **Next**
    - Go to this website and click in supertool
```text
https://mxtoolbox.com/SuperTool.aspx
```
    - Select ASN lookup and put ASN number. Now it provides CIDR range

- **If you want to calculate IP in CIDR range then go to**
```text
https://www.ipaddressguide.com/cidr
```

- **Now, How to scan this much IP range because it is difficult to scan one by one. But we have a tool called angry IP Scanner**
- **Open angry IP scanner and use first and last IP of following calculated IP**
```text
https://www.ipaddressguide.com/cidr
```

- **Note**
- In place of 
```text
 https://whois.arin.net/ui/ 
 ```
 - we can use
 ```text
 https://bgp.he.net/ 
 ```

## To directly get IP address
```text
ping facebook.com
```
- For only IPv4
```text
ping -4 facebook.com
```

## Some other beautiful website
```text
https://www.whoxy.com/
```
```text
https://lopseg.com.br/
```
```text
```text
https://whois.domaintools.com/
```

## How to find acquisition?
- To find acquisition, take help of chatgpt
- Go to chatgpt and searc
```text
Hey, I want a list of all acquisition by Meta or Facebook till now
```

- **Go to chrome web store and add extension**
```text
wappalyzer
```
- **next go with**
```text
https://builtwith.com/
```

## Use amass tool available in kali linux
```text
amass -h
amass intel -asn 32934
```