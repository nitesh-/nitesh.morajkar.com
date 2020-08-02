---
date: "2012-09-29"
slug: "importance-of-templating-engine"
title: "Importance of templating engine"
description: ''
image: '/images/blog/template-engine-importance.png'
---

{% img center https://encrypted-tbn1.gstatic.com/images?q=tbn:ANd9GcRJH81Ylz4QNY_lU3pdsTBDhuU43MRl2LNi4JF7LYVQhiJ38pjPdQ %}

I worked as freelance web developer back in 2009-2010. I had just started learning PHP. I usually mixed my PHP code with the HTML code. Since the websites were quite basic, i didn't face maintainance problems.

Later I worked on a personal project [HelloAssignment](http://helloassignment.com) which<!-- more --> is a hub for engineering students in Mumbai, India to share assignments, write-ups. I wrote the entire code for HelloAssignment.com. In this project too, i mixed PHP code with HTML code. I faced lot of maintainance problems. Whenever new feature has to be added, You need to go through entire code and search for the place to insert the code. This was very boring.

I read about templating engines in **PHP** but since **PHP** is somewhat slow so didn't feel appropriate to use a templating engine on top of it. My assumption was found to be wrong. I realized my mistake and quickly made a plan to introduce Templating system on HelloAssignment.com. Since HelloAssignment.com was in beta mode and code was also very short, I could easily introduce templating engine in it.

Now, i googled to know about templating engines which consume less resources. I found **Smarty** to suite my requirements. There are many templating engines in PHP but i planned to use **Smarty** since it is widely used, it's user community and good documentation.

**Smarty** has very similar syntax as PHP, so, took no time to learn it. I included all my HTML code in .tpl files and separated PHP code from it. So, i write my Business logic in PHP files and html code in .tpl files. I found maintaining my code so flexible and usndestood importance of Templatig engines.

Few tips on Templating engines:



	
  * It's not necessary to use **Smarty** as templating engine but to use a **templating e**ngine is necessary according to me.

	
  * Never write business logic in tpl files. Similarly, never write HTML code in PHP files.

	
  * Also check that there's no text before **<?php** tag. If you do so, it will be difficult for you send HTTP headers.





