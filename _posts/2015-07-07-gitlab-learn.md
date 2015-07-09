---
layout: post
title:  gitlab-learn
date:   2015-07-07 12:55:11
category: "project management"
---
<p>操作系统环境：</p>
<pre>CentOS 6.5 x84_64 位 minimal

</pre>
<p>
环境部署，参考其他靠谱文档，建议官方文档，今天我们聊聊zabbix邮件告警的事。
项目即监控项，触发器相当于给监控项设置阈值，根据表达式触发触发器，产生报警。
关于操作系统CentOS6.0 以下版本都是通过mail命令调用sendmail的sm-client发送邮件，所以如果关闭sendmail按照很多网上的文档是发不出邮件的。
</p>
<p>那么mail命令如果仔细观察的话其实调用的是mailx来调用第三方非本地smpt服务。</p>

<h2>一.   首先卸载（或停止） senmail升级安装mailx</h2>
<h4>1)       停止sendmail:</h4>
<pre><code>
[root@localhost ~]# /etc/init.d/sendmail stop
[root@localhost ~]# chkconfig sendmail off
[root@localhost ~]#
</code></pre>
