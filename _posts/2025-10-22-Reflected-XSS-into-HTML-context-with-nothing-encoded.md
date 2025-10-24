---
title: Reflected XSS into HTML context with nothing encoded
description: Portswigger Academy XSS Lab
date: 2025-10-22 12:00:00
categories: [Lab Solution, Portswigger]
tags:
  [
    xss,
    lab,
    cross-site-scripting,
    injection,
    rxss,
    web-security-academy-xss,
    web-security-academy-xss-1,
  ]
render_with_liquid: false
media_subpath: /images/2025-10-22-Reflected-XSS-into-HTML-context-with-nothing-encoded
---

![Banner](portswigger_logo.png){: .rounded-10 .shadow}

# Lab: Reflected XSS into HTML context with nothing encoded

> #XSS1
{: .prompt-info}

> Lab Level : APPRENTICE
{: .prompt-warning}

> Lab Status : Solved
{: .prompt-tip}

## Lab Description :

This lab contains a simple reflected cross-site scripting vulnerability in the search functionality.

To solve the lab, perform a cross-site scripting attack that calls the alert function.

![Image-1](1.png){: .rounded-10 .shadow}

## Lab Solution :

After Accessing the lab,

- You will redirect to a simple web page.
- Here you will find **a search input box**

![2](2.png){: .rounded-10 .shadow}

- First Enter a Random Text `Unknown` and see where the text is reflected.
- It reflected on the `web page` and the `URL`.

![3](3.png){: .rounded-10 .shadow}

- After that try `HTML Injection`

```html
<i>Unknown</i>
```

![4](4.png){: .rounded-10 .shadow}

- Okey, `HTML Injection` is Confirmed.
- Now it's time for `Cross-Site Scripting`.

```html
<script>alert("XSS by Unkonwn");</script>
```
_stetst_

![5](5.png){: .rounded-10 .shadow}

- And that's it.

> Congratulations, you solved the lab!
{: .prompt-tip}

![6](6.png){: .rounded-10 .shadow}
