---
layout: post
title:  shell_cookbook_02
date:   2015-04-09 14:10:05
category: "linux_天使团"
---
<h2>第一节讨厌的正则</h2>


<h2 id="section1">之所以讨厌一个事物，是因为你驾驭不了它。</h2>
<h5 id="section1-1">一.乱七八糟的符号。</h5>
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

<h5>二.正则有什么用？</h5>

<p>1.查找匹配</p>


<p> 1)一个字符（如何在整篇文章中查找一个字符），正则提供了一些特殊符号，通过这
些符号去替换一些东西.</p>
<p>举例：在整篇文章中查找字母a</p> 
		
使用vi编辑器打开/etc/passwd 

<p>在末行模式下查找a 
</br>输入：/a/ 
</p> 
<p>比如要查找abc，是一个或的关系,那么用 [ ] 。</p>  
<p>输入  
</br>   ：/[abc]/    
</br>   ：/[a-c]/  
</br>   ：/a|b|c/
</p>

中括号，把你想要定位的东西写入里面。

`.`	任意一个字符.

`[]`  选择中括号里面的任意一个。 

`[^]`  取非，取反 

`[:alnum:]`阿尔法字符加数字 

`[:alpha:]`任意一个字符`[[:alpha]]` 

`[:digit:]`任意一个数字 `[[:digit:]]`（对它取反的话`[^[:digit:]]`）意为除了任意一个数字。 

`[:lower:]`小写。  

`[:upper:]`大写。

`[:space:]`空格。

`[:punct:]`标点。

* 总结`：`以上是如何定位一个字符。
