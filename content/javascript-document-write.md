---
date: "2012-09-28"
slug: "javascript-document-write"
title: "Javascript - document write"
description: ''
tags: ['js']
---

I chose to write about **document.write** because it is a basic method but has lot of impact on DOM. In this post, I will be focusing on basic part of **document.write**.

Most of us know that document.write is used to write content inside DOM. When you include a string in your JavaScript code and send it to the browser, everything that is part of the string is sent to the browser "as is". Once the browser receives your string from the `document.write()` method, it gets rid of <!-- more --> the `document.write()`, the parentheses, and double-quotes. Then it treats the rest, the part of the string, as HTML code. If the string that was sent is just text, the browser would display it. If you sent any special character, the browser would analyze it to find out if the character is a special HTML symbol. If it is, it would be treated appropriately. A script can result in complex code or difficult to interpret errors. Based on this, you can include any HTML tag as part of the string. Here is an example:

``` html
<script type='text/javascript'>
	document.write('Book Title: JavaScript Programming');
</script>
```

When the browser receives this script, it gets rid of everything that is not part of the string. After this operation, the remaining text becomes:

`Book Title: JavaScript Programming`

This is what the browser would try to display. As it happens, there is an HTML tag in the code, namely the break tag. Therefore, the break tag would be applied. Based on this, you can include any HTML tag as part of your script. Make sure you use the HTML tags appropriately. JavaScript will not correct or interpret your tags, it would send them as they are provided.

In the next part, I'll explain about why **document.write** is considered evil.
