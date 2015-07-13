---
layout: post
title:  shell_cookbook_05
date:   2015-07-10 10:55:11
category: "linux_天使团"
---
<h2>常用shell</h2>

<h2>查看TCP连接状态</h2>
<pre><code>
netstat -nat |awk 'NR>2 {print $0}' | awk '{print $6}' | sort | uniq -c | sort -rn
netstat -n | awk '/^tcp/ {++S[$NF]};END {for(a in S) print a, S[a]}'
netstat -n | awk '/^tcp/ {++state[$NF]}; END {for(key in state) print key,"\t",state[key]}'
netstat -n | awk '/^tcp/ {++arr[$NF]};END {for(k in arr) print k,"\t",arr[k]}'
netstat -n |awk '/^tcp/ {print $NF}'|sort|uniq -c|sort -rn
netstat -ant | awk '{print $NF}' | grep -v '[a-z]' | sort | uniq -c
</code></pre>
<p> awk 中的 $NF 相当于 $(NF) ($NF 和NF 区别)</p>
<pre><code>cat passwd | awk -F':' '{print $(NF)}'  // 等价于 cat passwd | awk -F':' '{print $7}'
</code></pre>
