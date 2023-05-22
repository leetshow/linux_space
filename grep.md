```-n	显示行号
-o	只显示匹配出来的内容
-rl	递归查询当前目录和其他子目录并返回文件名
-q	静默模式，无输出内容，可搭配echo $?查看是否执行成功
-A   数字	将匹配成功的行和其后面的几行都打印出来
-B   数字	将匹配成功的行和其前面的几行都打印出来
-C   数字	将匹配成功的行和其前后的几行都打印出来
--color=nerver/auto/always	以什么样的颜色打印出匹配成功的内容，nerver表示无颜色，auto和always大体相同，以常规颜色输出
-c	将匹配成功的行数输出
-E	等于Egrep，支持扩展正则表达式
-i	匹配时忽略大小写
-v	反向匹配，只匹配不包含此项的行
-w	匹配某单词
-s	不显示查询错误信息（目标不存在或目标无权访问等）
```

## -q 静默模式，无输出内容，可搭配echo $?查看是否执行成功

>  假设当前目录下有一个md文件

``` shell
ll |grep *.md
## resp
-rw-r--r--@ 1 bytedance  staff   124B May 22 15:37 grep.md
## if add -q args
ll |grep -q *.txt
## will resp nothing

```

## -v 反向匹配，只匹配不包含此项的行

> 假设当前目录下有grep.md、sed.md两个文件

```shell
ll |grep -v grep.md
total 8
-rw-r--r--  1 bytedance  staff     0B May 22 15:49 sed.md
ls |grep -c  md
2
```



## -E 正则匹配

```shell
 ls |grep -Ec  .d
2
```

