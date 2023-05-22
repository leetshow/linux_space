| 参数 | 功能                                                  |
| ---- | ----------------------------------------------------- |
| -n   | 只输出经过sed特殊处理的行                             |
| -i   | 对文件产生编辑行为，不加i默认是不会对原文件进行编辑的 |
| -e   | 直接在命令行执行sed编辑，多个命令可以用子命令分隔     |
| -r   | 指定使用扩展正则表达式                                |
| -f   | 指定执行某个文件内的sed指令                           |





## Replace String Using the sed Command

sed 's/old_string/new_string/' filename.txt

```
sed 's/box/bin/' sed.txt

Knox in bin.
Fox in socks.
Knox on fox in socks in bin.
Socks on Knox and Knox in bin.
Fox in socks on bin on Knox
```

## Replace All Occurrences of String Using the sed Command

如果一行里头有多处匹配，默认只匹配第一个命中的。除非加上g参数

```
sed 's/box/bin/g' sed.txt
```

## Replace Specific Occurrence in a Line Using the sed Command

如果希望替换第N个命中的关键字，可以加上数字



```
 sed 's/box/bin/2' sed.txt
```



## Only Print Lines With Substitute Text

By default, the **sed** command prints out the entire file content, along with the substitute text in its output. If you have a lot of text and want to focus on the lines with the applied changes, add the needed attributes to the command.



The **-n** option disables automatic printing, while the substitute command **p** instructs **sed** to print lines where substitution occurs.

You can add the **p** command to other substitute commands, as in the example below:

```
sed -n 's/box/bin/p' sed.txt
# 输出源文件内容和替换后的内容
Knox in bin.
Knox in bin.
Fox in socks.
Knox on fox in socks in bin.
Knox on fox in socks in bin.
Socks on Knox and Knox in bin.
Socks on Knox and Knox in bin.
Fox in socks on bin on Knox.Fox in socks on bin on Knox.


sed -n  '1 s/box/bin/p' sed.txt
Knox in bin.
```



## Replace String Using the sed Command and Ignore Case

```
sed 's/knox/bin/2ip' sed.txt
Knox in box.
Fox in socks.
Knox on fox in socks in box.
Socks on Knox and bin in box.
Socks on Knox and bin in box.
Fox in socks on box on Knox.
```



### Replace String in Specific Line Using the sed Command

```
sed  '1 s/box/bin/p' sed.txt
##范围删除，例如1~3行可以使用 sed  '1,3 s/box/bin/p' sed.txt
Knox in bin.
Knox in bin.
Fox in socks.
Knox on fox in socks in box.
Socks on Knox and Knox in box.
Fox in socks on box on Knox.%
```

### Delete Specific Line Using the sed Command

```
sed '2d' sed.txt
Knox in box.
Knox on fox in socks in box.
Socks on Knox and Knox in box.
Fox in socks on box on Knox.%

## delete 2,3,4 line
sed '2,4d' sed.txt

```



### Delete From Specific to Last Line Using the sed Command

```
 sed '2,$d' sed.txt
```

