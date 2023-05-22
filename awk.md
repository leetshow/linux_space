# 1. AWK Variables

##  $N

The **awk** command has built-in field variables, which break the input file into separate parts called **fields**. The **awk** assigns the following variables to each data field:

- **$0**. Used to specify the whole line.
- **$1**. Specifies the first field.
- **$2**. Specifies the second field.
- etc.

## NR

- **NR**. Counts the number of input records (usually lines). The **awk** command performs the pattern/action statements once for each record in a file.
- NR表示AWK当前处理的行数

```
awk '{print NR,$0}' awk.txt
1 a,1,1
2 b,2,1
```



## NF

- **NF**. Counts the number of fields in the current input record and displays the last field of the file.
- NF 每一行分割后的字段数量

```
awk -F ","  '{print $NF}' awk.txt
1
1
```

## FS

- **FS**. Contains the character used to divide fields on the input line. The default separator is space, but you can use **FS** to reassign the separator to another character (typically in **BEGIN**).
- AWK 默认对每一行的分隔符为空格，可以通过FS来替换

```
awk -FS 'BEGIN{fs=",";}{print $0}' awk.txt
a,1,1
b,2,1
```

## RS

**RS**. Stores the current record separator character. The default input line is the input record, which makes a newline the default record separator. The command is useful if the input is a comma-separated file

默认换行符作为一个行，可以通过RS设置来定义行的范围

```shell
cat student.txt
Jones
2143
78
84
77

Gondrol
2321
56
58
45

$cat student.awk
BEGIN {
	RS="\n\n";
	FS="\n";

}
{
	print $1,$2;
}

$ awk -f student.awk  student.txt

Jones 2143
Gondrol 2321
```

## OFS

- **OFS**. Stores the output field separator, which separates the fields when printed. The default separator is a blank space. Whenever the printed file has several parameters separated with commas, the **OFS** value is printed between each parameter.
- OFS 完成 行分割后的拼接部分

```
 awk -F ","  '{OFS="\t";print $1,$2,$3}' awk.txt
a	1	1
b	2	1
```



# 2. AWK Statements

## if-else

```
cat awk.txt
a,1,1
b,2,1%

awk -F ',' '{if ($2==$3){print $1","$2","$3}else {print "no"}}' awk.txt
a,1,1
no
```



## while



```
 awk '{i=0;while(i<=NF){print i ":"$i;i++;}}' awk.txt
0:a,1,1
1:a,1,1
0:b,2,1
1:b,2,1
```



## for



```
awk 'BEGIN{for (i=1;i<10;i++) print "the square of ", i,"is",i*i;}'
the square of  1 is 1
the square of  2 is 4
the square of  3 is 9
the square of  4 is 16
the square of  5 is 25
the square of  6 is 36
the square of  7 is 49
the square of  8 is 64
the square of  9 is 81
```



# 3. AWK Patterns

## Regular Expression Patterns

正则表达式，过滤出包含a开头的行数

```
 awk '$1 ~ /^a/ {print $0}' awk.txt
a,1,1
```



#### Special Expression Patterns

```
awk 'BEGIN{print "start.."};{print $0};END {print "end"}' awk.txt
start..
a,1,1
b,2,1
c,3,3
end
```



# AWK Actions

## How to Use the AWK Command - Examples

```
df | awk '/\/dev/ {print $1"\t"$2+$3}'
/dev/disk1s5s1	1022127856
devfs	1412
/dev/disk1s4	993268104
/dev/disk1s2	980230864
/dev/disk1s6	976703432
/dev/disk1s1	1580618360
/dev/disk1s5	1022127856
/dev/disk2s2	101920


awk 'length($0) > 8' /etc/shells



ps -ef |awk '{if ($NF== "--seatbelt-client=160") print $0}'
  501 99372   540   0  4:44PM ??         0:49.05 /Applications/Google Chrome.app/Contents/Frameworks/Google Chrome Framework.framework/Versions/113.0.5672.92/Helpers/Google Chrome Helper (Renderer).app/Contents/MacOS/Google Chrome Helper (Renderer) --type=renderer --metrics-client-id=8a3e30c1-718c-478a-b133-e62f6f587e0d --lang=en-US --num-raster-threads=4 --enable-zero-copy --enable-gpu-memory-buffer-compositor-resources --enable-main-frame-before-activation --renderer-client-id=4688 --time-ticks-at-unix-epoch=-1684292310518692 --launch-time-ticks=253990014952 --shared-files --field-trial-handle=1718379636,r,15355023856966043775,8781322183785028692,262144 --seatbelt-client=160
  
  
  awk '{ print "The number of characters in line", NR,"=" length($0) }' employees.txt


```





# 参考

https://stackoverflow.com/questions/16203336/simple-awk-command-issue-fs-ofs-related
https://phoenixnap.com/kb/awk-command-in-linux