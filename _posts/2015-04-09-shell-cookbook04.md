---
layout: post
title:  shell_cookbook_04
date:   2015-04-10 09:55:11
category: "linux_天使团"
---
<h2>第三节简单明了的输入输出.</h2>


<pre><code>echo
printf
cat
tee
read
</code></pre>
Fd重点！！！


<p>echo作用：主要用于输入，用在显示上。</p>
<p>echo用法：</p>
<p>语   法：<code>echo [-ne][字符串]</code>或 <code>echo [--help][--version]</code></p>
<p>补充说明：echo会将输入的字符串送往标准输出。输出的字符串间以空白字符隔开, 并在最后加上换行号.</p>
<pre>
参   数：-n 不要在最后自动换行 
      -e 若字符串中出现以下字符，则特别加以处理，而不会将它当成一般文字输出：
	 \a 发出警告声；
	 \b 删除前一个字符；
	 \c 最后不加上换行符号；
	 \f 换行但光标仍旧停留在原来的位置；
	 \n 换行且光标移至行首；
	 \r 光标移至行首，但不换行；
	 \t 插入tab；\v 与\f相同；
	 \\ 插入\字符；
	 \nnn 插入nnn（八进制）所代表的ASCII字符；
--help 显示帮助--version 显示版本信息
</pre>
举例
<code>echo -e "\033[32;49;1m [DONE] \033[39;49;0m"</code>或<code>echo -e "\e[32;49;1m [DONE] \033[39;49;0m"</code>

输出结果 ：<code>[DONE]</code>


<p>文本终端的颜色可以使用“ANSI非常规字符序列”来生成。</br>
举例：</p>

<pre><code>echo -e "\033[44;37;5m ME \033[0m COOL"</code></pre>

<p>以上命令设置背景成为蓝色，前景白色，闪烁光标，输出字符“ME”，然后重新设置屏幕到缺省设置，输出字符 “COOL”。“e”是命令 echo 的一个可选项，它用于激活特殊字符的解析器。“\033”引导非常规字符序列。“m”意味着设置属性然后结束非常规字符序列，这个例子里真正有效的字符是 “44;37;5” 和“0”。修改“44;37;5”可以生成不同颜色的组合，数值和编码的前后顺序没有关系。可以选择的编码如下所示：
</p>
编码 颜色/动作
<pre>
0 重新设置属性到缺省设置
1 设置粗体
2 设置一半亮度（模拟彩色显示器的颜色）
4 设置下划线（模拟彩色显示器的颜色）
5 设置闪烁
7 设置反向图象
22 设置一般密度
24 关闭下划线
25 关闭闪烁
27 关闭反向图象
30 设置黑色前景
31 设置红色前景
32 设置绿色前景
33 设置棕色前景
34 设置蓝色前景
35 设置紫色前景
36 设置青色前景
37 设置白色前景
38 在缺省的前景颜色上设置下划线
39 在缺省的前景颜色上关闭下划线
40 设置黑色背景
41 设置红色背景
42 设置绿色背景
43 设置棕色背景
44 设置蓝色背景
45 设置紫色背景
46 设置青色背景
47 设置白色背景
49 设置缺省黑色背景
</pre>

<h3>其他有趣的代码还有：</h3>
<pre>
\033[2J 　清除屏幕
\033[0q 　关闭所有的键盘指示灯
\033[1q 　设置“滚动锁定”指示灯 (Scroll Lock)
\033[2q 　设置“数值锁定”指示灯 (Num Lock)
\033[3q 　设置“大写锁定”指示灯 (Caps Lock)
\033[15:40H 把关闭移动到第15行，40列
\007 　　发蜂鸣生beep
</pre>

RedHat的字体和背景颜色的改变方法：

<p>命令：
<pre><code>PS1="[\e[32;1m\u@\h \W]\\$"</code></pre>
或</br>
<code>export PS1="[\e[32;1m\u@\h \W]\\$"</code> 两者的区别请查看环境变量的相关资料
</p>
解释：

<code>\e[32;1m：</code>这就是控制字体和背景颜色的转义字符，30~37是字体颜色、40~47是背景颜色

<p>例子中的32;1m数字的位置是可以对调的如\e[1;32m，如果是在X环境下可以更换一下1的范围0~10，可能有的没用处：0或者不写（\e[0;32m或\e[;32m）显示浅颜色，1：显示高亮 4：加下划线.....如果改后的效果不好，但是又还原不了，那就不写m前面的数字，如\e[32;m，或者直接注销再登陆</p>

 <h3>\u \h \W：这是一些转义字符，下面详细解释：</h3>
 <pre>
	\d ：代表日期，格式为weekday month date，例如："Mon Aug 1"
	\H ：完整的主机名称。例如：我的机器名称为：fc4.linux，则这个名称就是fc4.linux
	\h ：仅取主机的第一个名字，如上例，则为fc4，.linux则被省略
	\t ：显示时间为24小时格式，如：HH：MM：SS
	\T ：显示时间为12小时格式
	\A ：显示时间为24小时格式：HH：MM
	\u ：当前用户的账号名称
	\v ：BASH的版本信息
	\w ：完整的工作目录名称。家目录会以 ~代替
	\W ：利用basename取得工作目录名称，所以只会列出最后一个目录
	\# ：下达的第几个命令
	\$ ：提示字符，如果是root时，提示符为：# ，普通用户则为：$
	\n ：新建一行
</pre>
字体并不局限于一个颜色，可以有多个颜色：
<code>PS1="[\e[32;1m\u@\e[35;1m\h \e[31;1m\W]\\$"</code>

<p>以上两个命令在注销后再登陆就失效了，用下面方法使其永久生效：</p>
<code>vi /etc/profile</code>
在<code>“export PATH .....”</code>下面添加一行：<code>export PS1="[\e[32;1m\u@\h \W]\\$"`</code>
<p>注销再登陆，就成功了，如果没生效，使用source /etc/profile 命令试试，或者直接重启机器。</p>


<p>有些时候，需要为Linux服务的配置截个图，然后打印出来，结果在字符界面下就只有黑色背景，白色字体，打印出来费墨~~改改背景可能好点。</p>
<p>首先要知道在linux中，一些常用的颜色代码：(这些颜色是ANSI标准颜色)</p>
<p>前景色：30黑 31红 32绿 33黄 34蓝 35紫 36青 37白</p>
<p>背景色：40黑 41红 42绿 43黄 44青 45蓝 46青 47白</p>
前景颜色各数字是对应背景颜色减去10.
<p>命令：</p>  
<pre><code>echo -e "\033[background_number;foreground_numberm" </code></pre>

<p>如设置白色背景黑色前景字体应该是</p>  
<pre><code>echo   -e   "\033[47;30m"</code></pre>

<p>foreground_number=前景色</p>
<p>m要紧跟foreground_number，没有空格。</p>

<p>（说是白色背景，黑色字体。字体颜色我同意，可背景色咋看也不像是白色呀？o(∩_∩)o...）

\033   即退出键<esc>的ascii码(27),所以上面的命令也可写成如下形式
<pre><code>echo   "^[[47;30m"</code></pre>       
<p>其中的“^[”是先按ctrl-V,然后再按<esc>键（就是键盘左上角的键）产生的。</p>

<p>这种方法只能暂时改变一下，logout一下就没有了。不过可以vi /root/.bashrc, 在后面加上刚才的命令。</p>

<pre><code>echo -e '\033[47;30m'</code></pre>


<p>用的是终端控制字符，比如这个，就是光标跳到第60列，然后显示一个OK</p>
<pre><code>echo -en '\033[60G' && echo OK</code></pre>

<p>\033[就是终端转义字符开始，60G是命令。</p>
echo的-e选项就是让echo不自己处理终端转义字符
<p>内建命令echo 输出他的参数，以空格来分隔，以换行符来结束。返回值总为0。echo 使用的一些选项：</p>
<pre>
-e:转义反斜杠字符。
-n:禁止换行。
</pre>
<p>echo 命令使用的转义序列</p>
<p>	序列 意义</p>
<pre>
\a 闹铃
\b 退格
\c 强制换行
\e 退出
\f 清除屏幕
\n 新行
\r Carriage return.
\t 水平制表符
\v 垂直制表符
\\ 反斜杠
$#传递到脚本的参数个数
$*传递到脚本的参数，与位置变量不同，此选项参数可超过9个
$$脚本运行时当前进程ID号，常用作临时变量的后缀。如hash.$$
$!后台运行的&最后一个进程的ID号
$@与$#相同，使用时加引号，并在引号中返回参数的个数 
$-上一个命令的最后一个参数
$?最后命令的推出状态，0表示没有错误。其他任何值表示有错误。
echo 输出颜色需要恢复到之前，那么使用reset
</pre>



<p>printf 命令</p> 
<p>用途 </p>
</p>写格式化输出。 </p>
<p>语法</p> 
<pre>printf Format [ Argument  ... ] </pre>
</p>描述:</p> 
<p>printf命令转换、格式化并写 Argument参数到标准输出。Argument参数是由 Format参数控制格式化的。格式化输出行不能超出 LINE_MAX字节长度。</p>
<p>下列环境变量影响 printf命令的执行：</p> 
LANG 
<p>在 LC_ALL和相应的环境变量（以 LC_开头）没有指定语言环境时，确定语言环境编目使用的语言环境。</p>
LC_ALL 
<p>
确定用于覆盖由 LANG或其它任何 LC_环境变量设置的任何语言环境编目值的语言环境。
</p>
LC_CTYPE 
<p>确定把文本字节数据顺序解释为字符的语言环境；例如，单一字节对应多字节字符的参数。</p>
LC_MESSAGES 
<p>确定写消息使用的语言。</p>
LC_NUMERIC 
<p>确定数字格式编排的语言环境。此环境变量影响使用 e、E、f、g和 G转换字符编写的数字的格式。</p>
<pre>
*	Format参数是包含三种对象类型的一个字符串： 
*	无格式字符复制到输出流。 
*	转换规范，每个规范导致在值参数列表中检索 0 个或更多个项。
*	以下转义序列。在复制到输出流时，这些序列导致它们的相关操作在有此功能的设备上显示：
		// 反斜杠
		\a 警告
		\b 退格
		\f 换页
		\n 换行
		\r 回车
		\t 跳格 
		\v 垂直跳格
		\ ddd ddd是 1、2 或 3 位八进制数字。这些转义序列作为由八进制数指定的具有数字值的字节显示。
</pre>
<p>Argument参数是一个或多个字符串的列表，它在 Format参数的控制下被写到标准输出。</p> 
<p>
Format参数在必要的情况下会经常重新使用以满足 Argument参数。将好像提供了空字符串 Argument一样评估任何额外的 c 或者 s 转换规范；其它额外转换规范将好像提供了 0 Argument一样评估。此处 Format参数不包含转换规范仅出现 Argument参数，结果是不确定的。
</p>
<p>每个 Format参数中的转换规范都具有如下顺序的语法：</p> 
<pre>
1. % （百分号）。
2. 零或更多的选项，修改转换规范的含义。选项字符和它们的含义是：
　　- 转换结果在字段中左对齐。
　　+ 符号转换结果常以符号（+ 或者 -）开始。
　　空格如果符号转换的第一个字符不是符号，结果的前缀将是空格。如果空格和 + 选项字符都显示，则忽略空格选项字符。
　　# 此选项指定值转换到备用格式。对于 c、d、i, u 和 s 转换，选项没有作用。对于 o 转换，它增加精度来强制结果的第一数字是 a、0（零）。对于 x 和 X 转换，非零结果分别具有 0x 或 0X 前缀。对于 e、E、 f、g 和 G 转换，结果通常包含基数字符，即使基数字符后没有数字。对于 g 和 G 转换，结尾零不象通常一样除去。
　　0 对于 d、i、o、 u、x、e、 E、f、g 和 G 转换，前导零（跟在符号或底数的后面）用于填充字段宽度，将不用空格填充。如果显示 0（零）和 -（减号）选项，0（零）选项被忽略。对于 d、i、o、u、x 和 X 转换，如果指定精度，0（零）选项将被忽略。
　　注:
　　其它转换，没有定义其行为。
　　3. 可选的指定最小值字段宽度的十进制数字字符串。如果转换值字符少于字段宽度，该字段将从左到右按指定的字段宽度填充。如果指定了左边调整选项，字段将在右边填充。如果转换结果宽于字段宽度，将扩展该字段以包含转换后的结果。不会发生截断。然而，小的精度可能导致在右边发生截断。
　　4. 可选的精度。精度是一个．（点）后跟十进制数字字符串。如果没有给出精度，按 0（零）对待。精度指定：
　　* d、o、i、 u、x 或 X 转换的最少数字显示位数。
　　* e 和 f 转换的基数字符后的最少数字显示位数。
　　* g 转换的最大有效数字位数。
　　* s 转换中字符串的最大打印字节数目。
　　5. 指示要应用的转换类型的一个字符，例如：
　　% 不进行转换。打印一个 %（百分号）。
　　d, i 接受整数值并将它转换为有符号的十进制符号表示法。精度指定显示的最小数字位数。如果值转换后可以用更少的位数来表示，将使用前导零扩展。缺省精度是 1。精度为零的零值转换的结果是空字符串。用零作为前导字符来指定字段宽度，导致用前导零填充字段宽度值。
　　o 接受整数值并将它转换为有符号的八进制符号表示法。精度指定显示的最小数字位数。如果值转换后可以用更少的位数来表示，将使用前导零扩展。缺省精度是 1。精度为零的零值转换的结果是空字符串。用零作为前导字符来指定字段宽度，导致用前导零填充字段宽度值。不用八进制值表示字段宽度。
　　u 接受整数值并将它转换为无符号的十进制符号表示法。精度指定显示的最小数字位数。如果值转换后可以用更少的位数来表示，将使用前导零扩展。缺省精度是 1。精度为零的零值转换的结果是空字符串。用零作为前导字符来指定字段宽度，导致用前导零填充字段宽度值。
　　x, X 接受整数值并将它转换为十六进制符号表示法。字母 abcdef 用于 x 转换，字母 ABCDEF 用于 X 转换。精度指定显示的最小数字位数。如果值转换后可以用更少的位数来表示，将使用前导零扩展。缺省精度是 1。精度为零的零值转换的结果是空字符串。用零作为前导字符来指定字段宽度，导致用前导零填充字段宽度值。
　　f 接受浮点或者双精度值并将它转换为十进制符号表示法，格式为 [-] ddd.ddd。基数字符（在这里显示为十进制点）后的数字位数等于规定的精度。 LC_NUMERIC 语言环境编目确定在这个格式中使用的基数字符。如果不指定精度，则输出六个数字。如果精度是 0（零），将不显示基数字符。
　　e, E 接受浮点或者双精度值并将它转换为指数表示的形式 [-] d.dde{+|-}dd。在基数字符前有一个数字（在这里显示为十进制点），基数字符后的数字位数等于规定的精度。 LC_NUMERIC 语言环境编目确定在这个格式中使用的基数字符。如果不指定精度，则输出六个数字。如果精度是 0（零），将不显示基数字符。E 转换字符在指数前生成带 E 而不是带 e 的数字。指数通常至少包含两个数字。然而，如果要打印的指数值大于两个数字，必要时需要打印附加指数数字。
　　g、G 接受浮点和双精度值并转换为 f 或 e 转换字符的样式（或在 G 转换的情况下是 E），用精度指定有效数字的个数。尾零将从结果中除去。基数字符只有在其后是数字时显示。使用的样式取决于转换的值。样式 g 仅在转换的指数结果小于 -4，或大于或等于精度时使用。
　　c 接受值将其作为字符串并打印字符串中的第一个字符。
　　s 接受值将其作为字符串并打印字符串中的字符直到字符串结束或者达到精度指示的字符个数。如果没有指定精度，打印全部字符直到出现第一个空字符。
　　b 接受值将其作为字符串，可能包含反斜杠转义序列。打印来自转换字符串的字节直到字符串结束或者达到精度规范指示的字节数。如果没有指定精度，打印全部字节直到出现第一个空字符。
　　支持下列反斜杠转义序列：
　　* 先前列出的反斜杠转义序列在 Format 参数描述下。这些转义序列将被转换到它们表示的单个字符。
　　* \c（反斜杠 c）序列，它不显示并使 printf 命令忽略 Format 参数中的字符串参数包含的剩余的所有字符串，所有剩余的字符串参数和所有附加字符。
</pre>

<p>退出状态 <p>
<p>该命令返回以下出口值： <p>
0 
<p>成功完成。</p>
\>0 
<p>发生错误。</p> 
</p>示例 </p>
1. 输入下列命令：
<pre><code>printf "%5d%4d\n" 1 21 321 4321 54321</code></pre>
产生下列输出： 
<pre><code>
   1  21
  3214321
54321   0
 </code></pre>
<p>三次使用 Format参数打印所有给定字符串。0（零）由 printf命令提供以满足最后的 %4d 转换规格。</p>

2. 输入下列命令 :
<pre><code>printf "%c %c/n" 78 79</code></pre>
 
产生下列输出： 
<pre><code>7 7</code></pre>
 文件 
<code>/usr/bin/printf </code>
包含 printf命令

<p>printf 命令用来定制输出。</p>
<p>举例：</p>
<pre><code>
[root@localhost shell]# printf "%10d%10d\n" 1 1 3 4 2        
         1         1
         3         4
         2         0
[root@localhost shell]# printf "%5s%5s\n" 1 21 321 4321 54321 sss
    1   21
  321 4321
54321  sss
[root@localhost shell]# 
     
[root@localhost shell]# printf "%5d%5d\n" 1 21 321 4321 54321
    1   21
  321 4321
54321    0
[root@localhost shell]# 
</code></pre>
<p>观察以上输出的结果。提示输出的时候看显示的位数和定制位数的关系。</p>
<p>tee 命令：读取标准输入的数据，并将内容打印出来，生成文件。</p>

<code>tee file</code>

<p>如果文件不存在则创建，存在则覆盖。</p>
<pre><code>
[root@localhost shell]# cat ip | tee ip.bak
172.16.8.8 
172.16.9.9 
[root@localhost shell]#
</code></pre>
<code>tee -a</code>
<p>输出到标准输出的同时，追加到文件file中。如果文件不存在，则创建；如果已经存在，就在
末尾追加内容，而不是覆盖。</p>
<pre><code>
[root@localhost shell]# cat ip.bak
172.16.8.8 
172.16.9.9 
172.16.8.8 
172.16.9.9 
[root@localhost shell]# cat ip | tee -a ip.bak
172.16.8.8 
172.16.9.9 
[root@localhost shell]# cat ip.bak 
172.16.8.8 
172.16.9.9 
172.16.8.8 
172.16.9.9 
172.16.8.8 
172.16.9.9 
[root@localhost shell]#
</code></pre>
<code>tee -</code>
<p>重复输出字符串。后面跟多少个- 代表在本身输出的基础上加一次。看下面两个例子。</p>
<pre><code>
[root@localhost ~]# echo Hello | tee -
Hello
Hello
[root@localhost ~]# echo Hello | tee - -
Hello
Hello
Hello
[root@localhost ~]# echo Hello | tee - - -
Hello
Hello
Hello
Hello
[root@localhost ~]#
</code></pre>
<pre><code>
[root@localhost ~]# echo -n Hello | tee -
HelloHello[root@localhost ~]# echo -n Hello | tee - -
HelloHelloHello[root@localhost ~]# echo -n Hello | tee - - -
HelloHelloHelloHello[root@localhost ~]# 
</code></pre>

<p>read 命令：</p>
<pre>
1.基本读入
2.计时读入
3.默读（不显示在屏幕上）
</pre>
<p>这里只介绍基本读入，计时读入</p>

<p>基本读入:</p>
<p>接收标准输入（键盘）的输入，或其他文件描述符的输入,得到输入后，read命令将数据放入一个标准变量中。</p>
<p>简单的示例脚本：</p>
<pre><code>
#!/bin/bash
echo -n "Please input your name:"  //输入提示信息
read name		//读取输入，并赋给一个标准变量。
echo "Hello $name , welcome to my system" //打印出结果
exit 0  //退出shell程序。
</code></pre>
<p>read 本身内置了提示功能，加 -p参数即可实现上面的内容。</p>
<pre><code>
#!/bin/bash
read -p "Please input your name:" name  
echo "Hello $name , welcome to my system" 
echo Thank you "$name ! "
exit 0
</code></pre>
<p>注意这里的read部分最后一个name前面的空格。可以认为 -p “”是一个部分 read name是一个部分</p>

<p>计时读入：</p>
<p>使用read命令存在着潜在危险。脚本很可能会停下来一直等待用户的输入。如果无论是否输入数据</p>
<p>脚本都必须继续执行，那么可以使用-t选项指定一个 计时器。-t选项指定read命令等待输入的秒数。</p>
<p>当计时满时，read命令返回一个非零退出状态;</p>
 
<pre><code>#!/bin/bash
 
if read -t 5 -p "please enter your name:" name
 then 
 
    echo "hello $name ,welcome to my script"
 else
 
    echo "sorry,too later！"
 fi
 exit 0
 </code></pre>
 <p>其他参数：</p>
<p> -n参数限制字符输入，超过-n 指定的字符数，自动跳出。</p>
<pre><code>
[root@localhost shell]# read -n 5 -p "Enter you choice :" choice
Enter you choice :hello[root@localhost shell]#
 </code></pre>
<p>-s 参数隐藏你的输入。</p>
<pre><code>
[root@localhost shell]# read -s -p "Enter your number:" number
Enter your number:[root@localhost shell]# echo $number
123456
[root@localhost shell]# 
 </code></pre>
<p>在numuber后面输入内容是不显示的。</p>
<p>安全终端：stty 通过一个脚本来演示：</p>
<pre><code>#!/bin/bash
echo "Enter you password:"
stty -echo
read password
echo your password is "$password"
stty echo
</code></pre>

<p>执行过程：</p>
<pre><code>
[root@localhost shell]# sh sh7.sh 
Enter you password:
your password is testtest
</code></pre>
<p>文件的非交互式读取：</p>
<p>举例1：</p>
<pre><code>
#!/bin/bash
while read ip;do
        ping -c 1 $ip
wait
done</root/shell/ip
</code></pre>
<p>注：wait是父进程等待子进程运行完成之后再启新的进程。</p>

<p>执行结果:</p>
<pre><code>
[root@localhost shell]# sh sh8.sh 
PING 127.0.0.1 (127.0.0.1) 56(84) bytes of data.
64 bytes from 127.0.0.1: icmp_seq=1 ttl=64 time=0.017 ms

--- 127.0.0.1 ping statistics ---
1 packets transmitted, 1 received, 0% packet loss, time 0ms
rtt min/avg/max/mdev = 0.017/0.017/0.017/0.000 ms
PING 172.16.56.1 (172.16.56.1) 56(84) bytes of data.
64 bytes from 172.16.56.1: icmp_seq=1 ttl=255 time=1.21 ms

--- 172.16.56.1 ping statistics ---
1 packets transmitted, 1 received, 0% packet loss, time 0ms
rtt min/avg/max/mdev = 1.218/1.218/1.218/0.000 ms
[root@localhost shell]# 
</code></pre>
<p>举例2：用来操作两个变量</p>
<pre><code>
#!/bin/bash
while read ip1 ip2
do
        echo "one:$ip1 two:$ip2"
done</root/shell/ip
</code></pre>
<p>执行结果：</p>
<pre><code>
[root@localhost shell]# cat ip
127.0.0.1 8.8.8.8
172.16.56.1 202.106.0.20
[root@localhost shell]# sh sh9.sh 
one:127.0.0.1 two:8.8.8.8
one:172.16.56.1 two:202.106.0.20
[root@localhost shell]#
</code></pre>
<p>总结一下read：</p>
<pre>
1.需要人参与的输入
2.不需要人参与的输入
</pre>			

<p>输入输出重定向：</p>
<p>清空你将要导入对象的内容并写入 >前面命令的执行结果。</p>
<p>举例：</p>
<pre><code>
[root@localhost shell]# cat ip
172.16.6.6 
[root@localhost shell]# printf "172.16.8.8 \n" > ip  
[root@localhost shell]# cat ip
172.16.8.8 
[root@localhost shell]#
</code></pre>
<p>\>> 追加到你将要导入的对象的结尾，不改变对象本身的内容，把>>前面命令执行的结果写入。</p>
举例：
<pre><code>
[root@localhost shell]# cat ip
172.16.8.8 
[root@localhost shell]# printf "172.16.9.9 \n" >> ip  
[root@localhost shell]# cat ip
172.16.8.8 
172.16.9.9 
[root@localhost shell]#
</code></pre>
<p>< 读取文件内容，更多的时候为避免人为的书写。</p>
举例：
<code>
[root@localhost ~]# cat < shell/ip 
172.16.8.8 
172.16.9.9 
[root@localhost ~]# 
</code>


<p>&lt;&lt;读取内容到指定的字符出现。</p>
<p>举例：</p>
<pre><code>
[root@localhost shell]# cat ip &lt;&lt;EOF &gt;ip.bak
> EOF
[root@localhost shell]# cat ip.bak 
172.16.8.8 
172.16.9.9 
[root@localhost shell]# cat &lt;&lt;EOF  &gt;file1
> look ! very beautiful !
> yes !
> I kown !
> EOF
[root@localhost shell]# cat file1 
look ! very beautiful !
yes !
I kown !
[root@localhost shell]#
</code></pre>

<p>以上的EOF是可以自定义的。</p>
举例：
<pre><code>
[root@localhost shell]# cat &lt;&lt;MZNH&gt;file2
 Hello ! meizi!
 Hi boy !
 can I help you ?
 yes!
 let't go my home.....
 MZNH
[root@localhost shell]# cat file2 
Hello ! meizi!
Hi boy !
can I help you ?
yes!
let't go my home.....
[root@localhost shell]#
</code></pre>
<p>从<<开始直到遇到MZNH结束交互。</p>




<p> | 管道：将第一条命令的输出，作为第二条命令的输入</p>
<code>command1 | command2</code>
<p>经常配合xargs使用：</p>
<pre><code>
[root@localhost shell]# echo a b c | xargs -n 1
a
b
c
[root@localhost shell]# echo a b c | xargs -n 3
a b c
[root@localhost shell]# echo a b c | xargs -n 2
a b
c
[root@localhost shell]# 
</code></pre>


<p>tac 命令：反过来查看一个文件。其他用法自己研究一下。</p>
<pre><code>
[root@localhost shell]# cat file2 
Hello ! meizi!
Hi boy !
can I help you ?
yes!
let't go my home.....
[root@localhost shell]# tac file2 
let't go my home.....
yes!
can I help you ?
Hi boy !
Hello ! meizi!
[root@localhost shell]# 
</code></pre>

<p>（）合并输出：</p>
<pre><code>
[root@localhost shell]# cat file1 ; cat file2 >> file3
look ! very beautiful !
yes !
I kown !
[root@localhost shell]# cat file3 
Hello ! meizi!
Hi boy !
can I help you ?
yes!
let't go my home.....
[root@localhost shell]# (cat file1 ; cat file2)>file4
[root@localhost shell]# cat file4 
look ! very beautiful !
yes !
I kown !
Hello ! meizi!
Hi boy !
can I help you ?
yes!
let't go my home.....
[root@localhost shell]# 
</code></pre>

<p>文件描述符：</p>
 <p>>前面的2代表的是错误的输出。>前面1代表的是错误的输出。</p>
<pre><code>
[ITnihao@localhost ~]$ find / -name passwd 2&gt;/tmp/err
/selinux/class/passwd
/selinux/class/passwd/perms/passwd
/usr/bin/passwd
/etc/pam.d/passwd
/etc/passwd
[ITnihao@localhost ~]$ find / -name passwd 1&gt;/tmp/rig
find: “/root”: 权限不够
find: “/lost+found”: 权限不够
find: “/home/think”: 权限不够
find: “/home/zabbix”: 权限不够
find: “/usr/lib64/audit”: 权限不够
find: “/etc/selinux/targeted/modules/active”: 权限不够
find: “/etc/sudoers.d”: 权限不够
find: “/etc/polkit-1/localauthority”: 权限不够
find: “/etc/audisp”: 权限不够
............
</code></pre>



思考：查看一个系统中没有的文件。echo $?的返回值是多少？
<pre><code>[root@localhost ~]# ls /etc/chaojihuai
ls: 无法访问/etc/chaojihuai: 没有那个文件或目录
[root@localhost ~]# echo $?
[root@localhost ~]# ls /etc/chaojihuai
ls: /etc/chaojihuai: 没有那个文件或目录
[root@localhost ~]# ls /etc/chaojihuai 2>&1 | grep --color "没有"
ls: /etc/chaojihuai: 没有那个文件或目录
[root@localhost ~]# 
</code></pre>
<p>总结以上可以看出：错误的信息是不经过管道的。
备注：由于代码没有找到高亮方法，这里grep --color 输出的结果中的“没有”
应该是红色的。</p>

--------------------------------------------------------------
<p>在linux中每启动一个程序或者脚本，都会在系统/proc/下产生一个与PID该名字相对应的目录，这个目录下有个目录叫fd存放与之相关的文件描述符。</p>
<pre><code>
#!/bin/bash
echo "the shell pid $$"
ls -l /proc/$$/fd/
echo "sleep 3s"
sleep 3
echo "link 4 -> /tmp/fdtestwrite"
exec 4> /tmp/fdtest
echo "list current fd"
ls -l /proc/$$/fd/
sleep 3
cat /etc/passwd >&4
sleep 3
echo "close /tmp/fdtest"
exec 4>&-
echo "list current fd"
ls -l /proc/$$/fd/
echo "sleep 3s"
sleep 3
echo "link 5 -> /tmp/fdtestread"
exec 5< /tmp/fdtest
echo "list current fd"
ls -l /proc/$$/fd/
sleep 3
echo "read file from fd5, exec grep command"
grep 'root' <&5
sleep 3
echo "close /tmp/fdtest"
exec 5<&-
echo "list current fd"
ls -l /proc/$$/fd/
sleep 3
</code></pre>
<pre>
*	exec 文件描述符> 建立关系文件 ，以读的形式建立关系。
*	exec 文件描述符>&- 取消建立关系。
*	exec 文件描述符< 以写的形式建立关系。
*	exec 文件描述符<&- 取消建立的关系。 
</pre>

fd的重要性。
<p>看一下下面的小例子：</p>
<pre><code>[root@localhost shell]# ps
  PID TTY          TIME CMD
20202 pts/3    00:00:00 bash
20716 pts/3    00:00:00 ps
[root@localhost shell]# ls -l /proc/20202/fd
总计 0
lrwx------ 1 root root 64 04-02 13:48 0 -> /dev/pts/3
lrwx------ 1 root root 64 04-02 14:39 1 -> /dev/pts/3
lrwx------ 1 root root 64 04-02 14:39 2 -> /dev/pts/3
lrwx------ 1 root root 64 04-02 14:39 255 -> /dev/pts/3
[root@localhost shell]# 
</code></pre>
pts指的是终端文件。
<pre><code>
[root@localhost shell]# echo hello > /dev/pts/3
hello
[root@localhost shell]# 
</code></pre>
<h5>和直接 echo hello的效果是一样的。</h5>
<p>玩一下两个终端的通信。开启两个终端，查看终端号。</p>

<p>第一个终端：</p>
<pre><code>[root@localhost ~]# ps
  PID TTY          TIME CMD
20732 pts/5    00:00:00 bash
20765 pts/5    00:00:00 ps
[root@localhost ~]# 
</code></pre>
<p>第二个终端：</p>
<pre><code>[root@localhost shell]# ps
  PID TTY          TIME CMD
20202 pts/3    00:00:00 bash
20768 pts/3    00:00:00 ps
[root@localhost shell]#
</code></pre>
<p>在一个终端输入：</p>
<pre><code>[root@localhost ~]# echo hello > /dev/pts/3
[root@localhost ~]# 
</code></pre>
<p>查看第二个终端：</p>
<code>[root@localhost shell]# hello </code>
<p>他会莫名奇妙打印出一个hello。</p>

<p>介绍一个命令：
lsof </p>

<p>-d 查看一个文件描述符被那些进程打开了。</p>
<pre><code>[root@localhost shell]# lsof -d 3 | grep "dev"  
udevd       597      root    3u  unix 0xde4e1e40      0t0       1862 socket
iscsid     2649      root    3u   CHR        1,3      0t0       1837 /dev/null
rpc.idmap  3277      root    3u   CHR        1,3      0t0       1837 /dev/null
automount  3464      root    3r   CHR      10,58      0t0      12175 /dev/autofs
dbus-laun  3828      root    3u   CHR        1,3      0t0       1837 /dev/null
gconfd-2   3836      root    3u   CHR        1,3      0t0       1837 /dev/null
[root@localhost shell]# 
</code></pre>
<p>-i 端口被那个进程打开的。</p>
<pre><code>
[root@localhost shell]# lsof -i:22
COMMAND   PID USER   FD   TYPE DEVICE SIZE/OFF NODE NAME
sshd     3499 root    3u  IPv6  12326      0t0  TCP *:ssh (LISTEN)
sshd     3499 root    4u  IPv4  12328      0t0  TCP *:ssh (LISTEN)
[root@localhost shell]#
</code></pre>
<p>+d 查看这个目录下的文件被那些进程打开。</p>
<pre><code>[root@localhost shell]# lsof +d /proc  
COMMAND    PID USER   FD   TYPE DEVICE SIZE/OFF       NODE NAME
vmtoolsd  2510 root   16r   REG    0,3        0 4026531842 /proc/meminfo
vmtoolsd  2510 root   17r   REG    0,3        0 4026531853 /proc/stat
vmtoolsd  2510 root   18r   REG    0,3        0 4026531857 /proc/vmstat
klogd     3149 root    0r   REG    0,3        0 4026531848 /proc/kmsg
Xorg      3751 root    6w   REG    0,3        0 4026532156 /proc/mtrr
lsof     21064 root    3r   DIR    0,3        0          1 /proc
[root@localhost shell]# 
</code></pre>
<p>+D 查看这个目录下的文件被那些进程打开，具体到子目录。</p>
<pre><code>[root@localhost shell]# lsof +D /proc  
COMMAND    PID      USER   FD   TYPE DEVICE SIZE/OFF       NODE NAME
vmtoolsd  2510      root   16r   REG    0,3        0 4026531842 /proc/meminfo
vmtoolsd  2510      root   17r   REG    0,3        0 4026531853 /proc/stat
vmtoolsd  2510      root   18r   REG    0,3        0 4026531857 /proc/vmstat
klogd     3149      root    0r   REG    0,3        0 4026531848 /proc/kmsg
acpid     3381      root    3r   REG    0,3        0 4026532165 /proc/acpi/event
hald      3394 haldaemon   11r   REG    0,3        0  222429201 /proc/3394/mounts
Xorg      3751      root    5u   REG    0,3      256 4026532298 /proc/bus/pci/00/0f.0
Xorg      3751      root    6w   REG    0,3        0 4026532156 /proc/mtrr
lsof     21066      root    3r   DIR    0,3        0          1 /proc
lsof     21066      root    6r   DIR    0,3        0 1380581385 /proc/21066/fd
[root@localhost shell]#
</code></pre>
<p>-c command 查看这个命令打开了那些文件，这些文件调用的进程。</p>
<pre><code>[root@localhost shell]# lsof -c ls
COMMAND   PID USER   FD   TYPE DEVICE SIZE/OFF       NODE NAME
lsof    21072 root  cwd    DIR  253,0     4096    4316938 /root/shell
lsof    21072 root  rtd    DIR  253,0     4096          2 /
lsof    21072 root  txt    REG  253,0   129820    9887131 /usr/sbin/lsof
lsof    21072 root  mem    REG  253,0   245376    3271583 /lib/libsepol.so.1
lsof    21072 root  mem    REG  253,0    93508    3271584 /lib/libselinux.so.1
lsof    21072 root  mem    REG  253,0   130864    3271547 /lib/ld-2.5.so
lsof    21072 root  mem    REG  253,0  1693820    3271566 /lib/libc-2.5.so
lsof    21072 root  mem    REG  253,0    20668    3271567 /lib/libdl-2.5.so
lsof    21072 root  mem    REG  253,0 56417488    9881339 /usr/lib/locale/locale-archive
lsof    21072 root    0u   CHR  136,3      0t0          5 /dev/pts/3
lsof    21072 root    1u   CHR  136,3      0t0          5 /dev/pts/3
lsof    21072 root    2u   CHR  136,3      0t0          5 /dev/pts/3
lsof    21072 root    3r   DIR    0,3        0          1 /proc
lsof    21072 root    4r   DIR    0,3        0 1380974601 /proc/21072/fd
lsof    21072 root    5w  FIFO    0,6      0t0     365144 pip
</code></pre>
 
<p>lsod找回误删除的文件。</p>
<p>恢复删除的文件</p>

><p>当 UNIX 计算机受到入侵时，常见的情况是日志文件被删除，以掩盖攻击者的踪迹。管理错误也可能导致意外删除重要的文件，比如在清理旧日志时，意外地删除了数据库的活动事务日志。有时可以恢复这些文件，并且lsof可以为您提供帮助。</p>

>当进程打开了某个文件时，只要该进程保持打开该文件，即使将其删除，它依然存在于磁盘中。这意味着，进程并不知道文件已经被删除，它仍然可以向打开该文件时提供给它的文件描述符进行读取和写入。除了该进程之外，这个文件是不可见的，因为已经删除了其相应的目录条目。

><p>前面曾在转到 /proc 目录部分中说过，通过在适当的目录中进行查找，您可以访问进程的文件描述符。在随后的内容中，您看到了lsof可以显示进程的文件描述符和相关的文件名。您能明白我的意思吗？</p>

></p>但愿它真的这么简单！当您向lsof传递文件名时，比如在`lsof /file/I/deleted`中，它首先使用stat()系统调用获得有关该文件的信息，不幸的是，这个文件已经被删除。在不同的操作系统中，lsof可能可以从核心内存中捕获该文件的名称。清单 5显示了一个 Linux 系统，其中意外地删除了 Apache 日志，我正使用grep工具查找是否有人打开了该文件。</p>

<p>在 Linux 中使用 lsof 查找删除的文件</p>
<pre><code>
# lsof | grep error_log
httpd      2452     root    2w      REG       33,2      499    3090660
/var/log/httpd/error_log (deleted)
httpd      2452     root    7w      REG       33,2      499    3090660
/var/log/httpd/error_log (deleted)
... more httpd processes ...
</code></pre>

<p>在这个示例中，您可以看到 PID 2452 打开文件的文件描述符为 2（标准错误）和 7。因此，可以在 /proc/2452/fd/7 中查看相应的信息，如下代码：</p>

<p>通过 /proc 查找删除的文件</p>
<pre><code>
# cat /proc/2452/fd/7
[Sun Apr 30 04:02:48 2006] [notice] Digest: generating secret for digest authentication
[Sun Apr 30 04:02:48 2006] [notice] Digest: done
[Sun Apr 30 04:02:48 2006] [notice] LDAP: Built with OpenLDAP LDAP SDK
</code></pre>

><p>Linux 的优点在于，它保存了文件的名称，甚至可以告诉我们它已经被删除。在遭到破坏的系统中查找相关内容时，这是非常有用的内容，因为攻击者通常会删除日志以隐藏他们的踪迹。Solaris 并不提供这些信息。然而，我们知道httpd守护进程使用了 error_log 文件，所以可以使用ps命令找到这个 PID，然后可以查看这个守护进程打开的所有文件。</p>

<p>在 Solaris 中查找删除的文件</p>
<pre><code>
# lsof -a -p 8663 -d ^txt
COMMAND  PID   USER   FD   TYPE        DEVICE SIZE/OFF    NODE NAME
httpd   8663 nobody  cwd   VDIR         136,8     1024       2 /
httpd   8663 nobody    0r  VCHR          13,2          6815752 /devices/pseudo/mm@0:null
httpd   8663 nobody    1w  VCHR          13,2          6815752 /devices/pseudo/mm@0:null
httpd   8663 nobody    2w  VREG         136,8      185  145465 / (/dev/dsk/c0t0d0s0)
httpd   8663 nobody    4r  DOOR                    0t0      58 /var/run/name_service_door
(door to nscd[81]) (FA:->0x30002b156c0)
httpd   8663 nobody   15w  VREG         136,8      185  145465 / (/dev/dsk/c0t0d0s0)
httpd   8663 nobody   16u  IPv4 0x300046d27c0      0t0     TCP *:80 (LISTEN)
httpd   8663 nobody   17w  VREG         136,8        0  145466
/var/apache/logs/access_log
httpd   8663 nobody   18w  VREG         281,3        0 9518013 /var/run (swap)
</code></pre>

<p>我使用-a和-d参数对输出进行筛选，以排除代码程序段，因为我知道需要查找的是哪些文件。Name列显示出，其中的两个文件（FD 2 和 15）使用磁盘名代替了文件名，并且它们的类型为VREG（常规文件）。在 Solaris 中，删除的文件将显示文件所在的磁盘的名称。通过这个线索，就可以知道该 FD 指向一个删除的文件。实际上，查看/proc/8663/fd/15就可以得到所要查找的数据。</p>

<p>如果可以通过文件描述符查看相应的数据，那么您就可以使用 I/O 重定向将其复制到文件中，如cat /proc/8663/fd/15 > /tmp/error_log。此时，您可以中止该守护进程（这将删除 FD，从而删除相应的文件），将这个临时文件复制到所需的位置，然后重新启动该守护进程。</p>

<p>对于许多应用程序，尤其是日志文件和数据库，这种恢复删除文件的方法非常有用。正如您所看到的，有些操作系统（以及不同版本的lsof）比其他的系统更容易查找相应的数据。</p>
