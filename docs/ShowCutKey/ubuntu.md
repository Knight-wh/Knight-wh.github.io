# Linux

## ubuntu bash

`ctrl + alt + T` 打开终端

`xdg-open {file | URL}` 打开图片、pdf等

`ctrl + L` : clear bash

`nautilus .` 终端打开文件管理器

解除端口占用：

```bash
wh21@wh21-ubuntu:~$ sudo lsof -i:9999
COMMAND    PID USER   FD   TYPE  DEVICE SIZE/OFF NODE NAME
node    234164 wh21   22u  IPv6 2331020      0t0  TCP *:9999 (LISTEN)
wh21@wh21-ubuntu:~$ sudo kill 234164
```

## vim/vi

`vim filename` 创建文件

`i` 插入

`:wq` 退出编辑

---

```bash
wh21:~$ date
2022年11月07日 星期一 

wh21:~$ echo hello
hello

wh21:~$ which echo
/user/bin/echo

wh21:~$ pwd
/home/wh21

wh21:~/document$ ls -l
-rw-rw-r-- 1 wh21 wh21 159 11月 2 19:23 geo.cpp

# back to previous directory
wh21:~$ cd -

wh21:~$ cat < hello.txt > hello2.txt

wh21:~$ man ls

wh21@ubuntu:~$ sudo su
root@ubuntu:~# 
root@ubuntu:~# exit
wh21@ubuntu:~$
```
[more shell tool](https://missing.csail.mit.edu/2020/shell-tools/)

```bash
wh21@ubuntu:~$ foo=bar
wh21@ubuntu:~$ echo 'value is $foo'
value is $foo
wh21@ubuntu:~$ echo "value is $foo"
value is bar

wh21@ubuntu:~$ echo "we in $(pwd)"
we in /home/wh21

```

常用的命令 find && grep

```bash
# 历史的shell命令中，包含find的命令
history | grep find

# 遍历打印所有的目录
ls -R

tree
```

xargs等等