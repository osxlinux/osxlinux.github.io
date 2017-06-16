---
layout: post
title:  python_base_01 16:50
date:   2017-06-16
category: "python"
---

<h6>ARP分组格式</h6>
<pre><code><table class="tg">
  <tr>
    <th class="tg-yw4l">以太网目的地址</th>
    <th class="tg-yw4l">以太网源地址</th>
    <th class="tg-yw4l">帧类型</th>
    <th class="tg-yw4l">硬件类型</th>
    <th class="tg-yw4l">协议类型</th>
    <th class="tg-yw4l">硬件地址长度</th>
    <th class="tg-yw4l">协议地址长度</th>
    <th class="tg-yw4l">OP</th>
    <th class="tg-yw4l">发送端以太网地址</th>
    <th class="tg-yw4l">发送端IP地址</th>
    <th class="tg-yw4l">目的以太网地址</th>
    <th class="tg-yw4l">目的IP地址</th>
  </tr>
  <tr>
    <td class="tg-yw4l">6</td>
    <td class="tg-yw4l">6</td>
    <td class="tg-yw4l">2</td>
    <td class="tg-yw4l">2</td>
    <td class="tg-yw4l">2</td>
    <td class="tg-yw4l">1</td>
    <td class="tg-yw4l">1</td>
    <td class="tg-yw4l">2</td>
    <td class="tg-yw4l">6</td>
    <td class="tg-yw4l">4</td>
    <td class="tg-yw4l">6</td>
    <td class="tg-yw4l">4</td>
  </tr>
  <tr>
    <td class="tg-yw4l" colspan="3">&lt;-------------------以太网首部-----------------&gt;</td>
    <td class="tg-yw4l" colspan="9"><--------------------------28字节APR请求应答--------------------------------></td>
  </tr>
</table></code></pre>