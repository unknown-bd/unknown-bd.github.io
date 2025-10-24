---
title: The Bug Hunters Methodology Live by Jason Haddix
description: Json Haddix
date: 2025-10-24 12:00:00
categories: [Notes, Course Notes]
tags: [notes,course-notes]
render_with_liquid: false
media_subpath: /images/2025-10-24-The-Bug-Hunters-Methodology-Live-by-Jason-Haddix
image:
  path: banner.png
---

# The Bug Hunter's Methodology Live by Jason Haddix

## Day 01

### Template and Reporting

#### Template Musings

You can keep track of targets, status/workflow, common tool syntax, and common reporting templates:

**# Technical Issue - Cross Site Scripting**

- The resource `payments` in the parameter `month` is vulnerable to reflected cross-site scripting. Once authenticated if a user is passed the URL:
- `https://XXXX.com/payments?month=%3Cscript%3Ealert(%27XSS%27)%3C/script%3E`
- JavaScript will be executed against the person visiting the link.
- payload: 
```html
<script>alert('XSS')</script>
```

**# Impact**

Attackers can leverage XSS to target, phish, and impersonate users of the application. This is possible because the vulnerability allows the attacker to gain the user's trust by using exploit links that appear to be from the application `xxxx.com`.

In the context of this application, which handles highly sensitive user date, XSS attacks enable attackers to specifically target and access personally identifiable information (PII) of users. This poses a significant threat to the privacy and security of the affected individuals.

**# Reproduction**

- login (create a free account)
- visit the link to see the PoC alert

**# Developer and Remediation Notes**

1. Always treat all user input as untrusted data.
2. Never insert untrusted data except in allowed locations.
3. Always input or output-encode all data coming into or out of the application.
4. Always whitelist allowed characters and seldom use blacklisting of characters except in certain use 5. cases.
5. Always use a well-known and security encoding API for input and output encoding such as the `OWASP ESAPI` or other framework provided solutions.
6. Never try to write input and output encoders unless absolutely necessary. Chances are that someone has already written a good one.
7. Never use the DOM function `innerHtml` and instead use the functions `innerText` and `textContent` to
8. prevent against DOM-based XSS.
9. As a best practice, consider using the `HTTPOnly` flag on cookies that are session tokens or sensitive tokens.
10. As a best practice, consider implementing `Content Security Policy` to protect against XSS and other injection type attacks.
11. 10.As a best practice, consider using an auto-escaping templating system
12. As a best practice, consider using the `X-XSS-Protection` response header.

**# References (Decent but generic)**

- [https://www.owasp.org/index.php/Top_10_2013-A3-Cross-Site_Scripting_(XSS)](https://www.owasp.org/index.php/Top_10_2013-A3-Cross-Site_Scripting_(XSS)) [https://www.owasp.org/index.php/Cross-site_Scripting_(XSS)](https://www.owasp.org/index.php/Cross-site_Scripting_(XSS))
- [https://www.owasp.org/index.php/XSS_(Cross_Site_Scripting)_Prevention_Cheat_Sheet](https://www.owasp.org/index.php/XSS_(Cross_Site_Scripting)_Prevention_Cheat_Sheet)
- http://projects.webappsec.org/Cross-Site+Scripting
- https://www.cvedetails.com/vulnerability-list/opxss-1/xss.html

**# To enhance XSS security: (Better. More Detail. Specific)**

- While the field/parameter X inherits default framework protections from XSS, further validation and sanitization is needed to ensure it meets expected formats, length limits, and character sets. Consider whitelisting characters rather than blacklisting. Consider implementing DOMPurify an industry respected XSS sanitization library.
- Encode untrusted data before inserting it into HTML, JavaScript, CSS, or other contexts, using appropriate encoding methods. Use HTML entity encoding (<, >, etc.) or context-specific encoding libraries (e.g., OWASP Java Encoder) where possible.
- Safely manipulate the DOM by avoiding vulnerable methods like `innerHTML` and using safer alternatives such as `textContent` or `createTextNode`.
- Secure cookies by setting the `HttpOnly` flag to prevent client-side JavaScript access and the Secure flag to restrict transmission to secure connections.
- Implement a strict Content Security Policy (CSP) to restrict content loading and execution, specifying trusted sources and limiting inline scripts.
- Utilize auto-escaping templating systems that automatically encode untrusted data based on the output context.
- Enable the X-XSS-Protection response header with the value "`1; mode=block`" to activate the browser's XSS filter.

### Recon Intro

#### What are we after ?

- APEX Domain - twitch.tv
- Subdomain - [www.twitch.tv](http://www.twitch.tv/)
- IP Addresses
- Services

### ASNs

- ASNs will give us IP Addresses of owned servers
    - Those IPs will lead to more apex domains, websites, and servers
- ASN - Autonomous System Numbers.

### Shodan

- [Shodan](https://shodan.io/) - you can manually search for your target.
- [karma_v2](https://github.com/Dheerajmadhukar/karma_v2.git) - is a tool for shodan automation
- [WTFIS](https://github.com/pirxthepilot/wtfis) - is a tool for shodan automation
- [Shosubgo](https://github.com/incogbyte/shosubgo.git) - is a tool that will gather only subdomain from Shodan.

#### Other Shodan Resources :

- Official Shodan Documentation
    - [Data reference](https://datapedia.shodan.io/)
    - [List of search filters](https://www.shodan.io/search/filters)
    - [Query syntax](https://help.shodan.io/the-basics/search-query-fundamentals)
    - [Official Examples](https://www.shodan.io/search/examples)
- [The Shodan Pentesting Guide](https://community.turgensec.com/shodan-pentesting-guide/)
- [Cert.shand Shodan Recon with @GodfatherOrwa](https://www.youtube.com/watch?v=YoXM4m1VEM0)
- [Shodan Filters and Hacks](https://www.youtube.com/watch?v=GyZFM5IaH2Y)
- [100 Shodan Queries for Discovery](https://www.osintme.com/index.php/2021/01/16/ultimate-osint-with-shodan-100-great-shodan-queries)
- [Org filter dorks for technologies](https://mr-koanti.github.io/shodan#)
- [General other interesting queries](https://github.com/jakejarvis/awesome-shodan-queries)

### Acquisitions

- Use [https://www.crunchbase.com](https://www.crunchbase.com/) to find acquisitions.
- Another site for finding acquisitions - [https://aleph.occrp.org](https://aleph.occrp.org/)

### Cloud Recon

- Go to [sni-ip-ranges • Directory Lister](https://kaeferjaeger.gay/?dir=sni-ip-ranges) and download all directory
- Use this command `cat *.txt | grep -F ".domain.com" | awk -F'-- ' '{print $2}'| tr ' ' '\n' | tr '[' ' ‘| sed 's/ //’| sed 's/\]//’| grep -F ".dell.com“ | sort -u` and replace domain with your targeted site and you will find stuff.
- Alternative command - `cat *.txt | grep .domain.com | grep -oP "(?<=\[).*(?=\])" | tr ' ' '\n | grep -v "*" | sort -u`

### Reverse WHOIS

- Use [www.whoxy.com](http://www.whoxy.com/) for Reverse WHOIS

### Recon GPT

- Use ChatGPT to ask for Acquisitions
- Here are some tools
    - https://github.com/s0md3v/SubGPT
    - https://github.com/jhaddix/SubreconGPT

### Link Discovery

- Link Discovery using Burp Pro
- Katana - Tool for Crawling
- GoSpider - Tool for Crawling
- WayBackUrls - Tool for Crawling
- Hakrawler - Tool for Crawlig

### Ad / Analytics Relationship

- [https://builtwith.com](https://builtwith.com/)  - Technology Profiling Tool. They shell there database.
    - Go to the website
    - Add the extension
    - Visit the website that you want to know about relationship
    - Click on the Extension
    - Go to relationship tab (Find UA code Recommended)
    - And you will find all the possible relation company
- https://github.com/m4ll0k/BBTz/tree/master - In this repo you can use [getrelationship.py](http://getrelationship.py) to find Relationship between companies.

### Trademark, Terms of Service, Copyright, & Privacy Policy Recon (using Google)

Here some Google Dork.

- `"© 2019 Twitch Interactive, Inc."inurl:twitch`
- `"© 2018 Twitch Interactive, Inc."inurl:twitch`

### Subdomain Scraping

- Subdomain Scraping will give us passive subdomain information

There are bunch of website’s that crawl, monitor the internet. There job is to give a user there needed information whether it’s subdomain, Technology Profile and much more.

We can use this to find subdomain

- Google
    1. site:twitch.tv -www.twitch.tv
    2. `site:twitch.tv -www.twitch.tv -watch.twitch.tv`
    3. `site:twitch.tv -www.twitch.tv -watch.twitch.tv -dev.twitch.tv`
    4. And So on
- Amass
- Subfinder
- BBot
    - Command for BBot to extract subdomain

```bash
cat /root/.bbot/scans/{scan_name}/output.txt | grep -F '[DNS_NAME]’ | awk '{print $2}'
```

### GitHub Enumeration

GitHub Enumeration can give us passive subdomain, IP Address, Vulnerability Data and more.

- For subdomain finding - https://github.com/gwen001/github-subdomains
- GitHub Dork Maker - https://gist.github.com/jhaddix/1fb7ab2409ab579178d2a79959909b33
- A collection of tools to perform searches on GitHub - https://github.com/gwen001/github-search

### Subdomain Brute-Force

- First tool is - https://github.com/blechschmidt/massdns
- Another tool is - https://github.com/d3mondev/puredns
    - To run this PureDNS we need resolver. Here is the resolver repo - https://github.com/trickest/resolvers
    - You can use https://github.com/AlephNullSK/dnsgen/ this tool to  permutation

Favicon Recon : 

- Here is a tool for this - https://github.com/devanshbatham/FavFreak

## Day 01 End

---

## Day 02

### Book Recommendation : 

- The web application hacker handbook 2
- Real World Bug hunting
- Bug Bounty Bootcamp
- The Hacker Playbook 2
- Hands on Hacking
- Bug Bounty Playbook
- Hacking APIs

### Labs : 

- Web Security Academy
- PentesterLab
- HackTheBox
- VulnHub
- DVWAD

### Analyzing Concept (Layer)

- Open Ports and Services
- Web Hosing  Software
- Application Framework
- Application Custom Code or COTs
- Application Library (Usually JavaScript)
- Integrations

### Analyzing Concept (**Tech Profiling**)

Extension : 

- WhatRuns
- Wappalyzer
- Builtwith

### Analyzing Concept (**The Big Question**)

- How does the application pass data?
- How / Where does the application talk about users.
- Does the app have tenancy or user level.
- Does the app have a unique thread model?
- Has there been past security research and vulnerability
- How does the app framework handle specific vuln classes.

### Content Discovery : 

- Open Burp and intercept the traffic and walk the app as a normal user.
- Spider with Burp
- Tools `ferobuster` and `ffuf` is best for content discovary.
- Wordlist Directory - https://wordlists.assetnote.io/ and https://github.com/danielmiessler/SecLists
- Another way is to discover content discovery is https://hub.docker.com/. Just search for your targeted website and you will get something interesting.
- Content Discovery (Historical) - There are a combination of some tool and a command. Here are those :
    - https://github.com/digininja/CeWL
    - https://github.com/ameenmaali/wordlistgen
    - https://github.com/lc/gau

```bash
echo bugcrowd.com | gau | wordlistgen | sort -u
```
- Another tool for Historical Content Discovery : https://github.com/xnl-h4ck3r/waymore
- Recursive scan on `401`
    - https://example.com/admin → 401
    - https://example.com/admin/dashboard → 401
    - https://example.com/admin/dashboard/member → 200
- Content Discovery via Mobile App Leaks - https://github.com/dwisiswant0/apkleaks
- In JavaScript file look for : parameter, routers, secrets, domains.
- In JavaScript file, Find path with GAP : https://github.com/xnl-h4ck3r/GAP-Burp-Extension
- Burp Extension - https://portswigger.net/bappstore/0ab7a94d8e11449daaf0fb387431225b
- Nuclei Alternative - https://github.com/jaeles-project/jaeles
- Make sure you know How application pass data.
- Make sure how or where dose the app talk about users.
    - How : `UID` or `Email`, `username`, `UUID`
    - Where : `Cookie`, `API Calls`.
- Make sure you know How dose the application stores data.

Head Mapping - Where is most  vulnerability found.

- **Upload Function** : It can be document upload, profile upload or anything website take data from third party.
- **Content Type**
    - Looking for multi-part forms
        - Because you can upload shell, injection, and other
    - Look for content type XML
        - For XXE
    - Looking for content type json
        - API Vuln
- **API**
    - Look for Hidden mehtods
    - Lack of auth
- **Account Section**
- **Errors**
- **Passing Paths**
- **Help Chatbots**
- **AI Chatbots**

Best XSS Methodology 
- https://hss-opus.ub.ruhr-uni-bochum.de/opus4/frontdoor/deliver/index/docId/4522/file/diss.pdf 
- https://www.blackhat.com/docs/eu-14/materials/eu-14-Javed-Revisiting-XSS-Sanitization.pdf

- XSS Parameter :
    
    ```bash
     q
     s
     search
     id
     lang
     keyword
     query
     page
     keywords
     year
     view
     email
     type
     name
     p
     month
     image
     list_type
     url
     terms
     categoryid
     key
     login
     begindate
     enddate
    ```
    
- IDOR Video  - https://www.youtube.com/watch?v=2WzqH6N-Gbc

## Day 02 End