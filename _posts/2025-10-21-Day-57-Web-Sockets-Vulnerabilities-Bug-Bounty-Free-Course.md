---
title: Day-57 Web Sockets Vulnerabilities - Bug Bounty Free Course 
description: By Defronix Academy
date: 2025-10-21 12:00:00
categories: [Notes, YouTube Notes]
tags: [notes, youtube,youtube-notes, one-shot-youtube-video-notes, playlists]
render_with_liquid: false
media_subpath: /images/2025-10-21-Day-57-Web-Sockets-Vulnerabilities-Bug-Bounty-Free-Course
image:
  path: banner.jpg
---

Video Link : [Here](https://www.youtube.com/watch?v=nbHIH42lUk4)

Playlists Link : [Here](https://www.youtube.com/playlist?list=PLOJR6EhNalnu7hgxu7QhA9GrF9i23JX9A)

Web Sockets are bi-directional , full duplex communications protocol initiated over HTTP. They are commonly used in modern web application for streaming data. 

- On HTTP protocol : `HTTP - Unsecured | HTTPS - Secured`
- On Web Socket : `WS -  Unsecured and WSS Secured.`

101 - protocol are called **Switching Protocols**

Web Socket Key is randomly generated `base64` key. We can’t perform authenticated attack using this key. It means if we find the key we can’t do anything crazy.

HTTP connections are transactional and complete after request and response. But WSS or WS or Web Sockets are long lived and are bi-directional, message can be send in either direction. Web Socket Connections are initiated over HTTP.

Web Socket Connections are normally created using client-side JavaScript like the following : 

```javascript
var ws = new WebSocket("wss://normal-website.com/chat");
```

The `WSS` protocol established a **Web Socket over an encrypted TSL Connection**, while the `WS` protocol used an `unencrypted connection`.

### How to Identify Web Socket requests?

Open Developer Tool and go to Network Tab and sort Socket Traffic. If you find a request with `101` status code and `switching protocol` and The request header should contain `Connection : Upgrade` and `Upgrade : websocket` then it’s a Web Socket Request. and the website have implemented web socket.

You can perform attack like XSS, CSRF, SQLi, RCE and other web related attack on Web Socket.

[Portswigger Labs](https://portswigger.net/web-security/websockets) for furture learning

> Complete ✅
{: .prompt-tip}