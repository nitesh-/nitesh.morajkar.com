---
title: "Setup Microsoft Outlook custom domain for free email hosting"
date: "2014-02-09"
slug: "setup-microsoft-outlook-custom-domain-for-free-email-hosting"
description: 'Setup Microsoft Outlook custom domain for free email hosting'
image: '/images/blog/Microsoft-Outlook-logo.jpg'
tags: ['email', 'email hosting']
---

I used Dreamhost shared hosting which gave me free custom Gmail hosting. Since, Dreamhost was costlier than other cloud hosting providers, I decided to use AWS. 

AWS provided a free Micro instance for the first year. This solved my Web hosting problem, but<!-- more --> my emails were still hosted on Gmail. No doubt Gmail is awesome, it charged me for the service. I was in search of a free Email hosting and found Microsoft Outlook which provided a free Email hosting. That's it!! I decided to switch my emails to Microsoft Outlook.

Microsoft Outlook provides following features:

 - Email hosting
 - Calender
 - Groups
 - Maps
 - Skydrive
 - Photos
 
All services are free and can be offered from a custom domain or sub-domain.

So my next step was to configure my domain with Outlook

Step 1:
-------
Login with your **outlook.com account**.

Step 2:
-------
Go to <a href="https://domains.live.com/Signup/SignupDomain.aspx" target="_blank">https://domains.live.com/Signup/SignupDomain.aspx</a>

Provide the domain name in the box. Don’t forget to check "**Set up Outlook.com for my domain**" in "**Choose mail service for your domain**" on the same page.

<img src="/images/post-image/smo-1.jpg" width="750" height="250" />

Step 3:
-------
Now, you'll be redirected to **Review settings and accept agreement**

<img src="/images/post-image/smo-2.jpg" width="750" height="300" />

After reviewing the details, click on "**I Agree**"

Step 4:
-------

Now, You'll  be asked to verify your domain and setup MX records. So go to your domain registrar dashboard and **Add MX record** against your domain. The one underlined in red in the following screenshot has to added.

<img src="/images/post-image/smo-3-red.jpg" width="600" height="900" />

After making changes in your DNS dashboard, you'll have to wait for sometime, until DNS is propagating across the globe. It may take from few seconds to 48 hrs. After few seconds, Hit the "**Refresh**" button.

You'll be redirected to "**Add domain**" page after domain is verified.

<img src="/images/post-image/smo-4.jpg" width="650" height="150" />

Step 5:
-------

Now, setup the email account. You can create up to **50 accounts** in your domain.

<img src="/images/post-image/smo-5.jpg" width="400" height="" />

After creating the account you may ask user to login and accept the T&C. Also their will be an account reset question for your users, which will be asked at first login.

And you're done.
