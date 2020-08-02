---
date: "2012-10-27"
slug: "how-to-install-a-python-module"
title: "How to install a python module"
description: "how to install a python module"
image: '/images/blog/install-python-module.jpeg'
tags: ['python']
---



Python doesn't provide all the modules by default. You can install a python module as explained:

<pre><code>cd ~/
# Check latest version if you wish
wget http://pypi.python.org/packages/source/s/setuptools/setuptools-0.6c11.tar.gz
tar -xzf setuptools-0.6c11.tar.gz 
cd setuptools-0.6c11 
python setup.py install</code></pre>
<!-- more -->
Now we have installed Setup tools. So, let us install required module. I'm considering installing MySQLdb module since it will give an example

Download from [http://sourceforge.net/projects/mysql-python/files/latest/download](http://sourceforge.net/projects/mysql-python/files/latest/download)

<pre><code>cd MySQL-python-x.y.z
python setup.py build
python setup.py install</code></pre>

The module is successfully installed. Now , you can import it in your Python script
