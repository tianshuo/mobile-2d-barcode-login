Mobile Scan Authentication and Interaction with Binded Device
=======================
A new way of authentication: Scan a barcode on your mobile phone to log in to supported sites. It also uses best practices in security. Please send send bug reports to tianshuo_at_gmail_dot_com  
Uses:

* qr codes
* html5 localstorage
* websockets

User needs:
* A phone with a camera and internet access
* Any QR code recognition software

Implemented in javascript(Node.js) welcome to port to other languages.

First time use case:
---
1. First time user scans a 2d barcode on a site using a mobile phone
2. On Phone, registers an account on our site
3. On phone, asks the user whether to connect this site (shows domain name using referer)
4. On webpage, automatically jumps to a page to connect with the user's original account or create new account (Site's account).

Normal use case:
---
1. User scans a 2d barcode on a site previously connected to
2. On phone, shows logged in to site
3. On webpage, site logs in automatically

Visit new site use case:
---
1. The user scans a 2d barcode on a new site
2. On phone, detect user is already logged in
3. On phone, asks the user whether to connect this site (shows domain name using referer)
4. On webpage, the site jumps to a page to connect with the user's original account.

Interaction use case:
---
1. The user scans a 2d barcode on site and logs in
2. Site displays remote control or other buttons on demand
3. Use Case: Pay XXX for XXX

Revoke Permission for site at:
---
Please access: http://xxxx/revoke

Lost your phone?
---
Please immediately access: http://xxxx/lost
You will be prompted to enter your username and password

Reset password?
---
Please access:
http://xxxx/forgotten
We will send you instructions to your email for resetting your password


Setting up for developers (Using our server):
---
Insert the below code inside your script:

    <script src="http://xxxx/login.js" async></script>
Setup using:

    mobilelogin.success(function(id){
    	// Log in
    });
    mobilelogin.revoked(function(err){
    	// Prompt user access revoked
    });
    mobilelogin.failure(function(err){
    	// Other failure
    });

In the background, our server will send a websocket request on logging in.

Setting up online payment and others:
---
Scenario where an account has money stored, and it needs a verification. 
You can also show text for the user and let the user enter their password on their phone again as double check.

Insert the below code inside your script:

    <script src="http://xxxx/check.js?text=Please pay $10 dolars for your book" async></script>


Setting up your own server:
---
Fork this code, edit to suit yourself. 
Get your own certificate


Security Internals:
---

* A salt for every user (TODO)
* Creates a random key for every device, can be revoked (TODO)
* Creates a random key for every site, site cannot steal access for other sites (TODO)
* Uses bcrypt, which is much safer than MD5/SHA (TODO)
* Uses secure websockets (TLS), cannot be intercepted by 3rd party (TODO)
* Rejects common and weak passwords (TODO)
* Limits speed when brute forcing detected (TODO)


Known Bugs:
---
* A computer may decode the qr code and simulate a phone (is that really a bug?)
* Hacker may steal key from localstorage cache on phone


Roadmap:
---
1. Make documentation <-- We're here now
2. Make first demo
3. Create qr code dynamically
4. Tighten security
5. Script for developers
6. Administrative interface
7. Show text as payment method
8. Change interface on mobile, on demand from web page
9. Support Oauth?
10. Mobile app?