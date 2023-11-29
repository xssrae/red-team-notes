---
tags:
  - API
  - WEB
---
# The Completely Ridiculous API (crAPI)

[https://github.com/OWASP/crAPI](https://github.com/OWASP/crAPI)

```
$mkdir ~/lab

$cd ~/lab

sudo curl -o docker-compose.yml https://raw.githubusercontent.com/OWASP/crAPI/main/deploy/docker/docker-compose.yml

$ sudo docker-compose pull

$ sudo docker-compose -f docker-compose.yml --compatibility up -d
```

If you are having issues installing this locally you can try the development version described here: [https://github.com/OWASP/crAPI](https://github.com/OWASP/crAPI) OR target the one that is hosted by APIsec.  
  
Once the installation is finished, you should be able to check to make sure crAPI is running by using a web browser and navigating to [http://127.0.0.1:8888](http://127.0.0.1:8888) (crAPI landing page) or [http://127.0.0.1:8025](http://127.0.0.1:8025)  (crAPI Mailhog Server). When you are done using/testing crAPI, you can stop it with docker-compose by using the following command:  
$sudo docker-compose stop

# vAPI

vAPI will be used for many of the assessments throughout this course. Although APIsec will be hosting vAPI, it may be useful to have a local version for testing.

vAPI: [https://github.com/roottusk/vapi](https://github.com/roottusk/vapi) 

```shell
$cd ~/lab  
$sudo git clone [https://github.com/roottusk/vapi.git](https://github.com/roottusk/vapi.git)  
$cd /vapi  
$sudo docker-compose up -d

to stop:
$sudo docker-compose stop
```

Once vAPI is running you can navigate to http://127.0.0.1/vapi to get to the vAPI home page. One important thing to note is that vAPI comes with a prebuilt Postman collection and environment. You can access these in the vAPI/postman folder.    
![](https://kajabi-storefronts-production.kajabi-cdn.com/kajabi-storefronts-production/site/2147573912/products/H29aKnQQRDOJpNBHHGJv_postman1.png)

You can import these into Postman to be prepared for testing for future assessments. Simply open Postman, select the Import button (top right), and select the two vAPI JSON documents (see above image). Finally, confirm the import and select the Import button.

![](https://kajabi-storefronts-production.kajabi-cdn.com/kajabi-storefronts-production/site/2147573912/products/7hfeGAPTtuy1XsdNnUqg_postman2.png)

One more thing to note about vAPI is that the Resources folder contains secrets that will be necessary to complete certain attacks. The resources folder can be found here.

![](https://kajabi-storefronts-production.kajabi-cdn.com/kajabi-storefronts-production/site/2147573912/products/H9dTPd6TRsWCNxIAQVDX_postman3.png)

There are many labs that are available to test out the tools and techniques that you learn in this course. Check out some of these other vulnerable labs:

**Portswigger**

- [Web Security Academy](https://portswigger.net/web-security)

**TryHackMe**

- [Bookstore](https://tryhackme.com/room/bookstoreoc) (free)
- [IDOR](https://tryhackme.com/room/idor) (paid)
- [GraphQL](https://tryhackme.com/room/carpediem1) (paid)

**[HackTheBox](https://www.hackthebox.com/hacker/hacking-labs) (Retired Machines)**

- Craft
- Postman
- JSON
- Node
- Help

**Github (Vulnerable Apps)**

- [Pixi](https://github.com/DevSlop/Pixi)
- [REST API Goat](https://github.com/optiv/rest-api-goat)
- [DVWS-node](https://github.com/snoopysecurity/dvws-node)
- [Websheep](https://github.com/marmicode/websheep)

You will get the most out of this course by getting your hands on the keyboard and hacking APIs. After you've learned a new tool or technique, I highly recommend applying your skills to these other labs.