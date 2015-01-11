---
layout: post
category: linux
---
###Linux下的四个命令: grep、find、sed和awk
朋友让我帮忙写一个python脚本: 找出一个目录下所有的`.txt`文件然后将它们的文件名写入一个文件中. 我所想的是这样一个任务应该不需要动用牛刀, 用linux命令就可以解决. 然而我一时并没有想出来怎么写这个命令, 后来初步学习了下`grep`, `find`, `sed`, `awk`这四个命令, 最后用`ls`, `grep`, `sed`这三个命令组合解决了这个问题：
{% highlight bash %}
ls -R | grep '\.txt$' | sed 's/\.txt$//g' > results
{% endhighlight %}
这条命令是这样执行的: 首先`ls -R`递归列出当前目录下的所有文件, 然后`grep`通过正则表达式匹配以`.txt`结尾的文件名, 朋友要求只要文件名, 不要`.txt`后缀, 于是用`sed`——同样是通过正则表达式匹配`.txt`后缀并将其替换为空——即删除`.txt`后缀, 最后将结果定向到`results`这个文件中.

看, linux就是这么简单(这只是我目前想到的写法, 也许还有更简单的) , 一行命令搞定一切! 我觉得有必要更深入的学习下这几个命令: 

####grep
grep从标准输入或指定的文件中找出所有与pattern匹配的行并打印.
用法:
{% highlight bash %}
grep [OPTIONS] 'PATTERN' [FILENAME]
{% endhighlight %}
我觉得几个比较有用的options:

- `-a`: 将二进制文档作为文本文档匹配
- `-c`: 计算找个匹配项的次数
- `-i`: 匹配时忽略大小写
- `-n`: 输出行号
- `-o`: 只输出没一行中被匹配到的部分
- `-v`: 反向匹配, 即输出没有匹配项的行
- `-A`: A后面可加数字, after的意思, 表示除列出该匹配行外指定数目的后面几行也列出来
- `-B`: 同上, B表示before, 列出前面的几行

####find
看名字就知道`find`是一个查找命令, 但不知道的是`find`有多强大！下面看它的基本用法:
{% highlight bash %}
find [PATH] [OPTION] [ACTION]
{% endhighlight %}
几个常用的选项：

- `-name`: 按文件名查找
- `-size`: 按文件大小查找
- `-mtime`: 按最近修改时间查找

下面看几个例子：

1.找出当前目录下(不指定路径默认为当前目录)所有`.py`文件:
{% highlight bash %}
find -name '*.py'
{% endhighlight %}
2.中出当前目录下一天内被更改过的文件:
{% highlight bash %}
find -mtime 0
{% endhighlight %}
上面的0代表当前的时间, 也就是从现在开始到24h前有更改的文件会被列出来. 这个参数还有不少花样, 比如说:

- `3`: 三天前的24小时内, 也就是3-4的那一天
- `+3`: 代表大于等于四天前
- `-3`: 代表小于等于四天内的档案

3.当我们找到想要的文件时可以通过`-exec`执行一些操作, 比如说再运行完一个python项目时会产生很多`.pyc`文件, 这时就可以通过下面这条命令清理这些文件:
{% highlight bash %}
find -name '*.pyc' -exec rm -f {} +   
{% endhighlight %}

####sed
参考这里: [sed简明教程][1]

####awk
参考这里: [awk简明教程][2]


[1]: http://coolshell.cn/articles/9104.html
[2]: http://coolshell.cn/articles/9070.html
