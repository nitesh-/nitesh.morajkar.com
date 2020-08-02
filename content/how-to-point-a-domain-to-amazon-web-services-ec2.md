---
title: "How to point a domain to amazon web services ec2"
date: "2013-06-01"
slug: "how-to-point-a-domain-to-amazon-web-services-ec2"
description: ''
image: '/images/blog/aws-ec2-domain-point.png'
tags: ['aws', 'ec2']
---

Once you have configured your Amazon web server, you need to point a domain to it. Here are the steps to configure:

**1. Create an Elastic IP:**
**Elastic IP** is the public IP address of your Amazon Instance. On the Amazon Dashboard,

 - Click **Elastic IPs** in the left hand menu.
 - On the top, Click on **Allocate New Address**.<!-- more -->
 - Now, you'll get a message prompt "Are you sure you want to allocate a new IP address?". Select **EIP used in EC2** and click on **Yes, Allocate**.
 - Click the checkbox next to the new IP address that has appeared in the main panel and press the **Associate Address** button in the top menu.
 - You'll get a prompt "Select the instance to which you wish to associate this IP address (xx.xx.xx.xx)". Select your machine instance and click on **Yes, Associate**.
 - Remember to check your **Public DNS** because it will be changed now.


**2. Setting up DNS:**
 
 - Add your public IP (xx.xx.xx.xx) against **A** Record of your DNS or you can also add **CNAME** record as **ec2-xx-xx-xx-xx.eu-west-2.compute.amazonaws.com**. 

After setting this, I tried to access my site but could not do so. So here comes the tricky step.

**3. Set HTTP rule in the security settings:**

 - Click on Security Groups.
 - Select user group. Now click on Inbound.
 - Select **HTTP** in **Create a new rule** dropdown and enter **0.0.0.0/0** in **Source**. Add this rule and click on "Apply Rule changes"

Now you should be able to access your site.

 
