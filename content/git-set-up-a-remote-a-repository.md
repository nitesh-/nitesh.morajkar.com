---
date: "2012-10-13"
slug: "git-set-up-a-remote-a-repository"
title: "Git - How to setup a git remote repository"
description: 'Git - How to setup a git remote repository'
image: '/images/blog/local-and-remote-git-repositories.jpg'
tags: ['git']
---



There are lots of search results on "How to setup a remote Git repository" on google. However, it's really tough to find proper link. Hence, I read couple of blogs on this article and<!-- more --> noted down key steps on this article. This posts is more of a note to self as I keep forgetting the steps needed to set up a GIT remote repository.

Let us first setup remote git repo
<pre><code>ssh username@hostname #username- Username of server, hostname - hostname of server
mkdir git-remote.git
cd git-remote.git
git init --bare # init bare repository
git update-server-info # if you plan to serve via HTTP
exit #exit/logout from remote server</code></pre>

Cool!! So, we have setup a remote repository. Now, let us push some files on the remote repository from our local machine.

<pre><code>mkdir ~/git-local
cd ~/git-local
git init # init repo
touch index.php #create a file
echo "" > index.php # edit the file
git add . # add all contents to git
git commit . -m "first_commit" # commit all files</code></pre>
We have create a local repository. So let us push all files to server

`git remote add origin username@hostname:git-remote.git`

`git remote add` just creates an entry in your git config that specifies a name for a particular URL. You must have an existing git repo to use this.

Lets push to remote repo

`git push -u origin master`

Suppose if you remember the username and host then you can following:

`git push username@hostname:git-remote.git`

Done.
