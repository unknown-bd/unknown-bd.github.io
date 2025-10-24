---
title: Ultimate Black Hat Hacking Course 2025 - Free and Comprehensive Guide
description: By AGT TechCore
date: 2025-10-21 12:00:00
categories: [Notes, YouTube Notes]
tags: [notes, youtube,youtube-notes, one-shot-youtube-video-notes]
render_with_liquid: false
media_subpath: /images/2025-10-21-Ultimate-Black-Hat-Hacking-Course-2025-Free-and-Comprehensive-Guide
image:
  path: banner.png
---

Video Link : [Here](https://www.youtube.com/watch?v=GjBTQnWwnLg)

## Malware
- REMCOS - Is a Trojan / Rat
  - But Windows Default Virous Protection will Detect it.
  - For this I use [Celesty file binder](https://github.com/GetBeamedbyGP/Celesty_Binder/releases/tag/Celesty). To bind the payload with other file like PDFs or Images.
  - Also Change The Icon using Celesty file binder

### Websites for checking Malware

- VirusTotal
- MetaDefender
- NoDistribute

### How malware Detected??

- There is a hash for every file. Whether you encrypted it or what ever you do the hash will remain same.
- The antivirus company research for malware and gain hashes , they make it into signatures compare it to your file and if it matches then the antivirus show alert.
- So we can do something so that the antivirus can’t calculate the hash.

![Malware-Juggler-Creation](malware-juggler-creation.png){: .shadow .rounded-10}

- To perform those operation that shows the upper image we are going to use Crypters.
  - Crypters Type
    - Public Stub
    - Privet Stub

## Ransomware

`1 : 45 : 44` - Ransomware maker name - NJRat. It has a feature of Trojan as well as Ransomware

### How to Check if you are effected to malware or not

- Method 01
    - Close every program that are connect to internet.
    - Open **Command Prompt**
    - Type `netstat -no`  and see your active connection. If you see something suspicious then you are hacked.
    - Check the `PID` and open task manager and find the service using `PID`. And end the task. But it’s not remove permanently.
    - To remove it permanently we are going to use some tools.
        - [TCPView](https://download.sysinternals.com/files/TCPView.zip)
        - [Autoruns](https://download.sysinternals.com/files/Autoruns.zip)
        - [ProcessExplorer](https://download.sysinternals.com/files/ProcessExplorer.zip)
    - Using one of the software if you see suspicious then you can check the Hacker’s IP. Grab the hacker’s IP and you can use any website to Track the IP.
        - https://www.iplocation.net/
        - https://www.ip-tracker.org/
    - Ok now we have confirm our computer is hacked. To remove malware permanently we are going to use `Autoruns` .
    - Open `Autoruns` . Every Blue Connection are verified. We look for the red connections.
    - `Right Click`on the Red Connection and `Delete`it.
- `2 : 33 : 25`  - `run vnc` is a command for Metasploit to  see Screen to the machine that you inject the payload.

### Phishing  
- [Online Phishing Tool](https://namirz.com)

### Email Gathering
- To gather email we are going to use `Email Extractor` you can search on google.

### Calling Scam
- Search any product in google.
- Go to their Facebook Page
- Grab their mobile number
- Call them and say their Facebook is violation Facebook Policy. And Grab their email.
- Send Facebook Phishing page in the email.

> Complete ✅
{: .prompt-tip}