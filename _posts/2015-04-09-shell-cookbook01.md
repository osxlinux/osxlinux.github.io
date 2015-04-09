---
layout: post
title:  shell_cookbook_讨厌的正则
date:   2015-04-09 14:10:05
category: "linux_天使团"
---
<h2>第一节讨厌的正则</h2>

<h5>之所以讨厌一个事物，是因为你驾驭不了它。</h5>

<p>乱七八糟的符号。</p>
(1)
   
举例：（grep  为行模式，默认以行显示）

<pre><code>[root@localhost ~]# cat /etc/passwd | grep --color "r..t"
root:x:0:0:root:/root:/bin/bash
operator:x:11:0:operator:/root:/sbin/nologin
ftp:x:14:50:FTP User:/var/ftp:/sbin/nologin
[root@localhost ~]# 
</code></pre>

<p>显示三行</p>

(2)
<pre><code>[root@localhost ~]# cat /etc/passwd | grep --color 'root'
root:x:0:0:root:/root:/bin/bash
operator:x:11:0:operator:/root:/sbin/nologin
[root@localhost ~]#
</code></pre>
<p>显示两行</p>
(3)
<pre><code>[root@localhost ~]# cat /etc/passwd | grep --color '^root'
root:x:0:0:root:/root:/bin/bash
[root@localhost ~]#
</code></pre>
<p>显示一行 </p> 

*	总结以上`:`什么是正则，两个单引号中间的部分就是正则。 

<h5>二.正则有什么用？<h5>
