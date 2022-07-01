### 字符编码

```
#查看编码
locale
#查看字符集
locale


```



### grep管道

```
cmd |grep content
#排除信息
grep -v content
# 支持正则
grep -v "contenta\|contentb"

```



开启正则

```shell
shopt -s
checkwinsize   	on
cmdhist        	on
expand_aliases 	on
extglob        	on
extquote       	on #正则
force_fignore  	on
histappend     	on
interactive_comments	on
progcomp       	on
promptvars     	on
sourcepath     	on
shopt -s extquote 开启
```


```
tar -c/-x 压缩/解压
-j/-z zip/gzip
-v 展示压缩/解压条目
-f 路径 解压压缩都需要
```

