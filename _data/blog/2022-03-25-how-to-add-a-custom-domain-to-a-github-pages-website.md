---
template: BlogPost
path: /custom-domain
date: 2022-03-25T22:47:18.766Z
title: How to Add a Custom Domain to a GitHub Pages Website
---
First after purchasing a domain, go to manage domain list.

* Add the following host records.

GitHub Pages domain record IP Addresses:

* Type: A Record | host: @ | IP: 185.199.108.153
* Type: A Record | host: @ | IP:185.199.109.153 
* Type: A Record | host: @ | IP:185.199.110.153
* Type: A Record | host: @ | IP:185.199.111.153
* Type: CNAME Record | host: www | username.github.io.

Go the github repo, which you want to host **\-> Settings -> Pages**

Custom Domain -> (Update the name of the domain here)  

* Before : [spattk.github.com/Portfolio](spattk.github.com/Portfolio)
* After: [siteshp.com](siteshp.com)
* Enable the HTTPS checkbox
* Click Save

By doing this, you can see, after opening https://siteshp.com, the page is blank.

If you face such problems, then follow the following steps
- Open package.json
- "homepage" key should be modified to the new domain name
- Before: "homepage" : "https://spattk.github.io/Portfolio
- After: "homepage" : "https://siteshp.com
- Deploy (npm run deploy)

Enjoy!
