---
layout: post
title:  python基础
date:   2015-04-09 17:40:05
category: "linux_天使团_python"
---
python基础环境

<h5><p>俗话说，工欲善其事必先利其器,学习任何一门知识或者语言,首先要具备良好的基础环境</p></h5>
<p>
配置一个属于自己的编程环境是相当重要的。</br>
环境：</br>
<li>操作系统：Ubuntu 14.04.2 LTS</br></li>
<li>	python软件：python2.7.9</br></li>
</p>
<pre>
<code>root@5bc95112c8c1:~# cat /etc/issue
Ubuntu 14.04.2 LTS \n \l
root@5bc95112c8c1:~# uname -r
2.6.32-431.el6.x86_64
root@5bc95112c8c1:~# uname -s
Linux
root@5bc95112c8c1:~# </code>
</pre>

<p>python软件<a href="https://www.python.org/downloads/">下载</a>.</p>

<pre>
<code>
root@5bc95112c8c1:~/workplace# wget https://www.python.org/ftp/python/2.7.6/Python-2.7.6.tgz
--2015-04-09 09:34:19--  https://www.python.org/ftp/python/2.7.6/Python-2.7.6.tgz
Resolving www.python.org (www.python.org)... 103.245.222.223
Connecting to www.python.org (www.python.org)|103.245.222.223|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 14725931 (14M) [application/octet-stream]
Saving to: 'Python-2.7.6.tgz'
51% [====================================================================>                                                                ] 7,639,144   96.4KB/s  eta 85s    ]
</code></pre>
<pre>
<code>
root@5bc95112c8c1:~/workplace# ls
Python-2.7.6.tgz
root@5bc95112c8c1:~/workplace#
</code></pre> 
解压python源码包：
<pre>
<code>
root@5bc95112c8c1:~/workplace# tar -zxf Python-2.7.6.tgz 
root@5bc95112c8c1:~/workplace#
</code></pre> 

<pre>
<code>
root@5bc95112c8c1:~/workplace# ls
Python-2.7.6  Python-2.7.6.tgz
root@5bc95112c8c1:~/workplace# 
</code></pre>
