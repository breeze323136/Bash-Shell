sh Shell脚本编程(一)
@(author:lianger)[from:www.sexyphp.com](http:www.sexyphp.com)

-------------------

[TOC]

####1.基础shell

#####1.1新建shell文件
命令:
>$ vim test.sh

文件：
```
#!/bin/shell
#第一行是说明基于哪个类型的shell脚本，目前学习的是基于bash shell脚本的编程
#"#"代表注释
echo $PATH
```
---------
#####1.2运行shell脚本
命令:
>$ sh test.sh

结果：
>MacBook-Air:~ lianger$ sh test.sh 
running shell script!


说明：
@`echo` 如同php 的echo命令差不多，输出字符串时需要加上单引号或双引号，如想在同一行显示一个文本字符串作为命令输出，可以使用echo -n参数

区分 `sh test.sh` 和 `./test.sh` 
`./test.sh` 如果.不在PATH里面，要执行当前目录下的可执行文件，使用全路径：./executable-file

 `sh test.sh`如果要执行一个sh脚本，不管那个脚本有没有可执行权限，都可以使用：
sh [file] 

---------

#####1.3使用变量:@`变量分为环境变量和用户变量，环境变量为linux自带的内置变量，用户变量则为用户自定义的变量。`

#####1.3.1 使用`set`获取环境变量

命令:
>$ set
 ---------
结果:
>MacBook-Air:~ VV$ set
Apple_PubSub_Socket_Render=/private/tmp/com.apple.launchd.5VgxiwGSv9/Render
BASH=/bin/bash
BASH_VERSINFO=([0]="3" [1]="2" [2]="57" [3]="1" [4]="release" [5]="x86_64-apple-darwin14")
BASH_VERSION='3.2.57(1)-release'
HISTFILE=/Users/vv/.bash_history
HISTFILESIZE=500
HISTSIZE=500
HOME=/Users/vv
HOSTNAME=MacBook-Air.local
HOSTTYPE=x86_64
 ---------
(1)使用变量之前需要加上美元符[$],如使用HOME,`echo $HOME`
(2)在双引号中使用特殊字符需要加上反斜杠，如输出$符号，`echo "\$"`
(3)说明:你可能见过${veriablename}形式引用变量。变量名两侧额外的花括号是帮助`$`符号识别变量名

#####1.3.2自定义变量
shell定义变量很简单，`variable name = variable value`,即变量名＝边变量值（如：var1=10）,不过变量的定义不允许超过20个字母，数字或下划线的文本字符串。`区分大小写`,与其他编程语言有区别的在于`变量名到变量值之间是不允许出现空格的`

`引用变量值时需要使用美元符，而引用变量来对其进行赋值时则不要使用美元符号，如下:`
 ---------
```
#!/bin/bash
#use variable descption
var1=10
var2=$var1
```
 ---------
####1.4 反引号(将shell命令赋给变量使用反引号｀｀)
如定义一个test变量，将date命令赋给test变量中
 ---------
```
$ cat
#!/bin/bash
#using the backtikc character
test=`date`
echo "The date and time are:" $test
``` 
 ---------
#### 1.5 重定向输入`<  <<`和输出`> >>`
就是将输入或输出的内容重定向到另一个位置。
 ---------
```
 >  将输出重定向到文件中，覆盖当前文件
 >> 将输出重定向到文件中，不覆盖当前文件

demo
$ date > file1.log

< 将文件的内容或者输入的内容重定向到命令中

<< 内联输入重定向，将输入内容重定向到命令中，必须指定一个文本标记来划分要输入数据的开始和结尾。

如

WC << EOF
> MYSQL
> PHP
> JAVA
> NODE.JS
> EOF
	 3     9     42
$

```
 ---------
#### 1.6 管道
将某个命令的输出作为另一个命令的输入

有时候将命令的输出重定向到文件有些繁琐，所以你可以重定向输出到另外一个命令，这个过程称为管道连接   `|`
 ---------
```
demo

ps -ef | sort

ls -l | more

```
 ---------

#### 1.7 shell执行数学运算
	
##### 1.7.1 expr命令   繁琐
 ---------
```bash
$ num1=2
$ num2=1
$ expr  $num1 + $num2   
$ expr  $num1 - $num2   
$ expr  $num1 \* $num2
$ expr  $num1 / $num2      
```
 ---------
#####1.7.2  使用方括号执行数学运算
 ---------
```
$ var1=$[1 + 5]
$ echo $var1
6

$ var2=$[$var1 * 5]
30
```
 ---------
#####1.7.3 浮点解决方案
(1)bc 计算器
bash计算器其实是允许你在命令行输入浮点表达式,解释表达式,计算并返回结果的一种编程语言

> bash计算器能实现的功能
> `整数和浮点数`
>  `变量（简单变量和数组）`
> `注释（＃或c风格的/* */）`
> `表达式`
> `编程语句`
> `函数`
 ---------
 
```
MacBook-Air:etc VV$ bc
bc 1.06
Copyright 1991-1994, 1997, 1998, 2000 Free Software Foundation, Inc.
This is free software with ABSOLUTELY NO WARRANTY.
For details type `warranty'. 

12 * 5
60

12 / 11    /* shell默认设置浮点数为0，如果需要设置浮点数后置几位数可以使用`scale＝0 ，如设置为保留4位小数点 scale=4` */
1

scale=4
12 /11
1.0909

12 / 12
1

/*退出bc计算器使用 quit*/
```
---------
(2) bc计算器在shell脚本中的使用(使用反引号)
基本格式：
---------
```
variable=`echo "options;expression" | bc`
//option 变量，多个变量用分号隔开
//expression 数学表达式
```
---------
文件：demo.sh
```
#!/bin/bash
var1=`echo "scale=4; 3.1415926 / 5" | bc`
echo The answer is $var1
```
result:
```
$ ./demo.sh
The anwser is .6283
```
---------
以上方式适合于简单的运算表达式，如果是复杂的运算表示的话，结合内联输入重定向，允许你直接在控制台重定向数据。

文件：
demo1.sh
---------
```
#!/bin/bash

var1=3.1415926
var2=43.567
var3=123.1234
var4=111

var5=`bc << EOF
scale = 5
a1 = ($var1 * $var2)
a2 = ($var3 * $var4)
a1 / a2
EOF
`

echo The final anwser for this mess is $var5
```

result:
```
$ ./demo1.sh
The final anwser for this mess is .01001
```
---------
@[desc:bash计算器中创建的变量只在bash计算器中有效，不能在shell脚本中使用，相当于局部变量]

#### 1.8 退出脚本

##### 1.8.1 查看退出状态 
Linux提供了`$?`命令专门来保存上一个执行命令的退出状态码,状态码最小和最大值为0～155

###Linux退出状态码
| status code     |  describe|  
| :-------- | --------:|
|	0  		|  成功		   |
|	1  		|  通用未知错误		   | 
|	2  		|  误用shell命令		   | 
|	126  		|  命令不可执行	   | 
|	127  		|  没找到命令			   | 
|	128  		|  无效退出参数		   | 
|	128+x  		|  Linux信号x的严重错误		   | 
|	130  		|  命令通过ctrl+c终止		   | 
|	255  		|  退出状态吗越界		   |  

---------
demo
```
$ date
2016年 3月26日 星期六 20时39分59秒 CST
$ echo $?
0


$ abnc
-bash: abnc: command not found
echo $?
127

//等学习到了条件判断的时候很有用，可以检测每个命令执行结束时返回的退出状态码，如果不等于0的情况下可视为执行该命令的状态错误而做其他的操作。
```
---------
##### 1.8.2 使用`exit`来改变退出的状态码

```
//当shell脚本执行完毕时，可根据自身状态设置退出状态码，如
exit 6

$ echo $?
6
```
---------
文件：
```
#!/bin/bash
var1=10
var2=20

var3=$[$var1 + $var2]
exit $var3
``` 
result:
```
$ sh demo.sh
echo $?
30
```

@[总结:]
以上都是基本且重要的shell命令，这是你开始你的shell编程时必不可少的基本功，希望有朋友跟我一起学习的话，可以反复练习以上命令，如果有任何不明白的地方可以在[www.sexyphp.com](http:www.sexyphp.com)留言或加笔者QQ一起学习和交流，哪儿有错误的地方，还希望前辈们给予纠正。

以上如有需要进一步了解的地方，可自行到百度搜索更多的相关知识进行深入了解。任何入门的知识，对于初学者来说，有些人觉得很难，有些人觉得很简单，有开心的，有激动的，有困惑的，希望大家找对方法，怀着渴望知识，好奇心等态度去学习，相信对你自己的收获更有帮助。

##下一节`流程控制命令[结构化]`






