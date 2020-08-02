---
date: "2012-10-13"
slug: "git-how-to-retrieve-deleted-files"
title: "Git - How to retrieve deleted files"
description: 'Git - How to retrieve deleted files'
image: '/images/blog/git-retrieve-deleted.jpeg'
tags: ['git']
---

I was working on a particular task for a project in my master branch. I made some changes to file demo.php. I wanted to revert the changes, so i deleted the file(rm -fr demo.php).<!-- more --> I didn't commit this change.

Now i was confused since i didn't know how to recover the file.

Normally, there can be two scenarios of retrieving a file.

**1) Retrieve a deleted file and the change has not been committed.**

Find the deleted files

`git ls-files --deleted`

In this case, simply use following command

`git checkout`

**2) Retrieve a deleted file and file has been committed.**

First you need to find the commit id

`git log`
#or
`git rev-list -n 1 HEAD -- `

You'll get a list of logs. Grab the latest commit id. and then

`git checkout ^ -- ;`

Your file will be retrieved.
