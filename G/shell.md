# shell

> 唔，想混着shell一块梭哈了（反正这俩也是一伙的，我是懒狗）
>
> 至于为什么做了两遍（因为有部分是实验课时候顺便摸了点）



```
cp		#拷贝
cp <参数> 源文件 目标文件
   -a	递归复制
   -i	覆盖前询问
   -b	覆盖前备份目标文件
   -f	强制覆盖
```

```
mv		#移动
mv <参数> 文件
   -b	当文件存在时, 覆盖前, 为其创建一个备份
   -f	若目标文件或目录与现有的文件或目录重复, 则直接覆盖现有的文件或目录
   -i	覆盖前先行询问用户
   -u	当源文件比目标文件新或者目标文件不存在时, 才执行移动操作
```

```
touch		#创建文件
```

```
mkdir		#创建文件夹
mkdir <参数> 目录
	  -p	若所要建立目录的上层目录尚未建立，则会一并建立上层目录
	  -m	<目标属性>或--mode<目标属性>建立目录的同时设置目录的权限
```

```
rm		#删除文件文件夹
rm <参数> file
   -f	强制删除文件或目录
   -i	删除文件或目录时先询问用户
   -r	删除当前目录下所有文件
```

```
chmod		#修改文件读写权限 
chmod <参数> 文件
	  -R : 修改当前目录下所有文件的权限
	  -v : 显示执行过程
```

```
chown		#修改文件所有者
chown <参数> 用户 文件
	  -R	将当前目录下所有文件的所有者都改为指定用户
	  -v	显示执行过程
```

```
echo		#输出字符，可以识别特殊变量

[root@localhost ~]$ echo hello world
hello world
[root@localhost ~]$ echo "111"
111

```

```
\		#转义字符，还原字符，使之不会被识别成特殊字符

[root@localhost ~]$ echo "111$PWD"
111/root
[root@localhost ~]$ echo "111\$PWD"
111$PWD
```

```
"双引号"	'单引号'
#双引号中会进行识别特殊变量
 单引号中不会
 
[root@localhost ~]$ echo "$PWD"
/root
[root@localhost ~]$ echo '$PWD'
$PWD
```

>**shell中的变量在定义的时候会赋予其值，脚本中的变量在shell执行完毕后，根据执行脚本的方式的不同，变量会消失或者保存。**
>
>当使用 bash 和 sh 的方式执行的时候，是开启子shell进程运行的。变量也是在子shell中加载，当子shell退出后，变量消失。
>
>当使用source 和 ./ 的方式执行脚本的时候，是在当前shell环境中加载变量，执行脚本。
>
>变量值的获取要加上 美元符号

```
$()

``		#执行内部命令，并拿出执行结果，两者同效果

[root@localhost ~]$ today = `date`
[root@localhost ~]$ echo $today
……………………（阿巴阿巴阿巴阿巴日期怎么用英文来着阿巴阿巴阿巴阿巴）

[root@localhost ~]$ today = $(date)
[root@localhost ~]$ echo $today
……………………
```

```
ll
ls -l
```



```
wc		#查看文件大小（ls：阿巴阿巴阿巴阿巴）
wc <参数> 文件
   -c(--bytes/--chars)	只显示Bytes数
   -l(--lines)	只显示列数
   -w(--words)	只显示字数
   
   
[root@localhost ~]$ wc -c miao.txt
92 test.txt
```

```
stat		#查看文件大小
stat <参数> 文件
	 -L	支持符号连接
	 -f	显示文件系统状态而非文件状态
	 -t	以简洁方式输出信息
	 
	 
[root@localhost ~]$ stat miao.txt
  文件："test.txt"
  大小：92        	块：8          IO 块：4096   普通文件
设备：fd02h/64770d	Inode：403222111   硬链接：1
权限：(0644/-rw-r--r--)  Uid：(    0/    root)   Gid：(    0/    root)
最近访问：2023-01-24 10:05:52.772435759 +0800
最近更改：2023-01-24 10:01:07.291855652 +0800
最近改动：2023-01-24 10:01:07.292855685 +0800
```

```
du		#这是一个一个一个
du <参数> <文件>
   -b(-bytes)	显示目录或文件大小时，以byte为单位
   -k(--kilobytes)	以KB(1024bytes)为单位输出
   -m(--megabytes)	以MB为单位输出。
   -h(--human-readable)	为输出数据添加单位(K，M，G)
   
   
[root@localhost ~]$ du -b G.txt
98	test.txt
[root@localhost ~]$ du -h G.txt
4.0K	test.txt
```

>【-eq】 : 等于(=)
>
>【-nq】 : 不等于(!=)
>
>【-gt 】: 大于(>)
>
>【-lt】   : 小于(<)
>
>【-ge】 : 大于等于(>=)
>
>【-le】  : 小于等于(<=)
>
>【-z】   : 字符串的长度是否为0, 使用方式为 [ -z “字符串” ]
>
>【-n】   : 字符串的长度是否大于0 ,使用方式为 [ -n “$STRING’”], 如果是变量外围一定要有双引号""

```
if		#判断
if [ 条件 ];then
elif [ 条件 ];then
else 
fi


栗子：
num=3
if [ $num = 1 ];then
  echo "first"
elif [ $num = 2 ];then
  echo "second"
else 
  echo "other"
fi
```

```
for循环
for (( i=0 ; i < length ; i++ ))
 
array=(1,2,3,4)
for ((i=0;i<${#array[@]};i++))
do 
  echo "${array[i]}"
done

-----------------------

for item in (1,2,3,4)

array=(1,2,3,4)
for item in ${array[*]}
do 
  echo "${item}"
done

------------------------
 for num in seq 1 5

for num in `seq 1 5`
do 
  echo $num
done

------------------------

```

```
while循环

num=1
while [ $num -gt 0 ]
do 
  echo "num > 0"
  num=`expr $num - 1`
done					

-----------------------------

while [ 1 ]
do 
  echo "死循环"
done				# 无限循环
```

```
break ( 结束循环 )
continue ( 跳过本次循环进入下一次循环 )
```



----

## linux操作

#### 1.文件操作

```
ls [选项] [目录名或文件名]		#查看目录和信息
   -d 只显示该目录信息
   -l  显示文件和文件的详细信息
   -a  显示目录下所有的文件，包括隐藏文件 .  （隐藏文件以英文句号“.”开头，     如 .bashrc）
   -h  显示文件大小
   -t  显示文件时间信息

[root@localhost ~]$ ls
Desktop    Downloads         Music     Public     test
Documents  examples.desktop  Pictures  Templates  Videos

------------------------------

ls -l		#查看根目录下文件和目录类型

[root@localhost ~]$ ls -l
total 48
drwxr-xr-x 2 catree catree 4096 Mar 20 02:35 Desktop
drwxr-xr-x 2 catree catree 4096 Mar 20 02:35 Documents
drwxr-xr-x 2 catree catree 4096 Mar 21 02:45 Downloads
-rw-r--r-- 1 catree catree 8980 Mar 20 02:33 examples.desktop
drwxr-xr-x 2 catree catree 4096 Mar 20 02:35 Music
drwxr-xr-x 2 catree catree 4096 Mar 20 02:35 Pictures
drwxr-xr-x 2 catree catree 4096 Mar 20 02:35 Public
drwxr-xr-x 2 catree catree 4096 Mar 20 02:35 Templates
drwxrwxr-x 2 catree catree 4096 Mar 21 02:47 test
drwxr-xr-x 2 catree catree 4096 Mar 20 02:35 Videos

# 第一列字母：
 'd'表示此为目录
 '-'表示此为普通文件
 'l'表示此为链接文件
```

```
pwd		#查看当前目录的绝对路径（相对路径就是那个和那个）

[root@localhost ~]$ pwd
/home/catree
```

```
touch 		#创建新文件

[root@localhost ~]$ ls
Desktop    Downloads         Music     Public     test
Documents  examples.desktop  Pictures  Templates  Videos
[root@localhost ~]$ touch hello
[root@localhost ~]$ ls
Desktop    Downloads         hello  Pictures  Templates  Videos
Documents  examples.desktop  Music  Public    test

[root@localhost ~]$ touch hello world
[root@localhost ~]$ ls
Desktop    Downloads         hello  Pictures  Templates  Videos
Documents  examples.desktop  Music  Public    test       world

#不对空格转义的人注定度过失败的一生（暴论）

```



```
mkdir		#创建新目录
	   -p	递归创建多个新目录（递归：你知道我要说什么了吧）
	   -m	创建新目录，并设置权限

[root@localhost ~]$ mkdir test1
[root@localhost ~]$ ls
Desktop    Downloads         hello  Pictures  Templates  test1 
Documents  examples.desktop  Music  Public    test       Videos

[root@localhost ~]$ mkdir -p test2/test3
[root@localhost ~]$ cd test2
[root@localhost ~]$ ls
test3
[root@localhost ~]$ -m 777 test4
```



```
rm		#删除文件或目录
rm [选项] 文件/目录
   -r	将指定目录与子目录递归删除
   -f	强制删除，忽略不存在的文件
   -rf  强制递归删除目录
   
[root@localhost ~]$ rm -r test2
[root@localhost ~]$ ls
Desktop    Downloads         hello  Pictures  Templates  test1 
Documents  examples.desktop  Music  Public    test       Videos

```



```
rmdir		#删除空文件名或目录名（选项上同）
```



```
mv		#移动文件或者目录（感觉跟剪切差不多）
mv [选项] 源文件/目录 目标文件/目录
	-i	若目标文件或目录存在，提示是否覆盖
	-f  强制覆盖
	
[root@localhost ~]$ touch 1.txt
[root@localhost ~]$ ls
1.txt Desktop    Downloads         hello  Pictures  Templates 
Documents  examples.desktop  Music  Public    test       Videos
[root@localhost ~]$ mv 1.test 2.txt
2.txt Desktop    Downloads         hello  Pictures  Templates  
Documents  examples.desktop  Music  Public    test       Videos
```



```
cp		#复制
cp [选项] 源文件/目录 目标文件/目录
   -p	复制的同时，复制源文件或目录属性
   -r	递归复制
   -i	若目标文件或目录存在，提示是否覆盖
   -a	-p+-r（你懂~~~~~）
   -f·强制覆盖
```

```
cat		#喵（bushi）查看文件内容
	-n	对输出的所有行从1开始编号
```

```
more
more [选项] 文件名
	 	+n	从n页开始查看
	 	-n	一页显示n行
	 	+/string	显示内容前搜索字符串string。隐藏前面内容								（...skiping），从string前两行开始显示
	 	
	 	
文件打开后:
【空格键】向下滚动一页
【Enter】向下滚动n行
【Ctrl + B】向上滚动一页
【Ctrl + F】向下
【q】退出
```

```
less		#more它爹来啦（bushi）
less [选项] 文件名
	 -e	文件显示结束后退出less
	 -i	搜索字符串时忽略大小写
	 -m	下方显示百分比
	 -N	显示行号
	 

文件打开后:
【空格键】向下滚动一页
【Enter】向下滚动一行
【pageup】向上滚动一页
【pagedown】向下滚动一页
【q】退出
【/string】向下搜索string
【?string】向上搜索string
【n】重复前一个字符串搜索
【N】反向反复前一个字符串搜索
```

```
tail		#查看末尾n行内容（默认10行）
tail [选项] 文件名
	 -n<行数>      显示文件末尾n行内容		
	 -f		      循环读取文件
	 -c<字节数>	显示末尾c个字节数
	 -s			  循环读取的间隔
```

```
head		#跟上面反过来（默认行数一样）
head [选项] 文件名
	 -n<行数>
	 -c<字节数>
```

---

#### 2.用户和用户组权限

```
useradd		#创建新用户
useradd [选项] [选项值] 用户名
		-d	指定用户的家目录
		-g	指定用户所属用户组
		-u	指定uid
		-m	自动创建家目录
		

[root@localhost ~]$ useradd -m -d /home/testuser1
Usage: useradd [options] LOGIN
       useradd -D
       useradd -D [options]

Options:
  -b, --base-dir BASE_DIR       base directory for the home directory of the
                                new account
  -c, --comment COMMENT         GECOS field of the new account
  -d, --home-dir HOME_DIR       home directory of the new account
  -D, --defaults                print or change default useradd configuration
  -e, --expiredate EXPIRE_DATE  expiration date of the new account
  -f, --inactive INACTIVE       password inactivity period of the new account
  -g, --gid GROUP               name or ID of the primary group of the new
                                account
  -G, --groups GROUPS           list of supplementary groups of the new
                                account
  -h, --help                    display this help message and exit
  -k, --skel SKEL_DIR           use this alternative skeleton directory
  -K, --key KEY=VALUE           override /etc/login.defs defaults
  -l, --no-log-init             do not add the user to the lastlog and
                                faillog databases
  -m, --create-home             create the user's home directory
  -M, --no-create-home          do not create the user's home directory
  -N, --no-user-group           do not create a group with the same name as
                                the user
  -o, --non-unique              allow to create users with duplicate
                                (non-unique) UID
  -p, --password PASSWORD       encrypted password of the new account
  -r, --system                  create a system account
  -R, --root CHROOT_DIR         directory to chroot into
  -s, --shell SHELL             login shell of the new account
  -u, --uid UID                 user ID of the new account
  -U, --user-group              create a group with the same name as the user
  -Z, --selinux-user SEUSER     use a specific SEUSER for the SELinux user mapping
      --extrausers              Use the extra users database
```

```
userdel		#删掉，删掉，一定要删掉（
userdel [选项] 用户名
		-r 删除用户时，将家目录一并删除


[root@localhost ~]$ userdel -r testuser1
[root@localhost ~]$ ls -l /home/testuser1
ls: cannot access '/home/testuser1': No such file or directory
```

```
usermod		#创建用户信息
usermod [选项] [选项值] 用户名 
		-d			修改家目录
		-e<有效期限> 修改用户有效期限
		-g			修改用户所属用户组
		-u			修改uid	
		-L			锁定用户密码
		-U			解锁用户密码
```



```
groupadd		#创建用户组
groupadd [选项] 用户组名
		 -g	指定用户组id
		 
		 
groupdel		#盯~~~~


passwd		#密码114514
passwd [选项] 用户名
	   -d	删除用户密码
	   -x	设置密码有效期
	   -g	修改用户组的密码
```

> 用户和群组的相关信息存放于四个文件中：/etc/passwd	/etc/shadow	/etc/group	/etc/ggroup	/etc/passwd

```
guest-xjodif@ubuntu:~$ cat /etc/passwd
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
games:x:5:60:games:/usr/games:/usr/sbin/nologin
man:x:6:12:man:/var/cache/man:/usr/sbin/nologin
lp:x:7:7:lp:/var/spool/lpd:/usr/sbin/nologin
mail:x:8:8:mail:/var/mail:/usr/sbin/nologin
news:x:9:9:news:/var/spool/news:/usr/sbin/nologin
uucp:x:10:10:uucp:/var/spool/uucp:/usr/sbin/nologin
proxy:x:13:13:proxy:/bin:/usr/sbin/nologin
www-data:x:33:33:www-data:/var/www:/usr/sbin/nologin
backup:x:34:34:backup:/var/backups:/usr/sbin/nologin
list:x:38:38:Mailing List Manager:/var/list:/usr/sbin/nologin
irc:x:39:39:ircd:/var/run/ircd:/usr/sbin/nologin
gnats:x:41:41:Gnats Bug-Reporting System (admin):/var/lib/gnats:/usr/sbin/nologin
nobody:x:65534:65534:nobody:/nonexistent:/usr/sbin/nologin
systemd-timesync:x:100:102:systemd Time Synchronization,,,:/run/systemd:/bin/false
systemd-network:x:101:103:systemd Network Management,,,:/run/systemd/netif:/bin/false
systemd-resolve:x:102:104:systemd Resolver,,,:/run/systemd/resolve:/bin/false
systemd-bus-proxy:x:103:105:systemd Bus Proxy,,,:/run/systemd:/bin/false
syslog:x:104:108::/home/syslog:/bin/false
_apt:x:105:65534::/nonexistent:/bin/false
messagebus:x:106:110::/var/run/dbus:/bin/false
uuidd:x:107:111::/run/uuidd:/bin/false
lightdm:x:108:114:Light Display Manager:/var/lib/lightdm:/bin/false
whoopsie:x:109:117::/nonexistent:/bin/false
avahi-autoipd:x:110:119:Avahi autoip daemon,,,:/var/lib/avahi-autoipd:/bin/false
avahi:x:111:120:Avahi mDNS daemon,,,:/var/run/avahi-daemon:/bin/false
dnsmasq:x:112:65534:dnsmasq,,,:/var/lib/misc:/bin/false
colord:x:113:123:colord colour management daemon,,,:/var/lib/colord:/bin/false
speech-dispatcher:x:114:29:Speech Dispatcher,,,:/var/run/speech-dispatcher:/bin/false
hplip:x:115:7:HPLIP system user,,,:/var/run/hplip:/bin/false
kernoops:x:116:65534:Kernel Oops Tracking Daemon,,,:/:/bin/false
pulse:x:117:124:PulseAudio daemon,,,:/var/run/pulse:/bin/false
rtkit:x:118:126:RealtimeKit,,,:/proc:/bin/false
saned:x:119:127::/var/lib/saned:/bin/false
usbmux:x:120:46:usbmux daemon,,,:/var/lib/usbmux:/bin/false
catree:x:1000:1000:树猫,,,:/home/catree:/bin/bash
guest-xjodif:x:999:999:Guest:/tmp/guest-xjodif:/bin/bash

#用户名、uid、gid、家目录、shell环境
```

#### 文件和目录访问控制

```
chown		#修改文件或目录的属主和属组
chown [选项] 用户名[:用户组名] 文件名或目录名
	  -R	递归修改目录及其子目录和文件
	  -v	显示执行过程
	  
	  
chmod		#修改用户或用户组对文件（或目录）读写执行权限
chmod [选项] mode 文件名或目录名
	  -R	递归修改目录及其所有子目录和文件
	  -v	显示执行过程
```

>文件信息前9个字符的标志位，分为三组，分别代表属主、属组、其他用户和用户组对该文件的执行权限：
>
>【r】读权限
>【w】写权限
>【x】可执行权限
>每一类标志位都有对应的数值，r是4，w是2，x是1
>
>
>
>1. mode有字符和数字两种形式`
>2. 字符：[ugoa] [+-=] [rwx]`
>3. u：文件属主，g：文件属组，o其他属主和属组，a：所有属主和属组`
>4.  +：增加某个权限，-删除某个权限，=唯一设定权限`
>5. r：读权限，w：写权限，x：可执行权限`

---

## 3.磁盘管理

```
df		#文件系统整体磁盘使用量
df [选项] [挂载目录或文件名]
   -a	列出所有文件系统磁盘使用量信息
   -k	以KB为单位显示文件系统磁盘使用量信息
   -m	以MB为单位显示文件系统磁盘使用量信息
   -h	综合使用GB，MB，KB单位，自行显示文件系统易读的磁盘使用量信息
   -T	显示文件系统的类型，如ext3
   -i	以inode的数量显示
```

```
du		#文件或者目录的磁盘空间使用量
du [选项] 文件名或目录名
   -a 列出所有的文件和目录容量
   -h 综合使用GB，MB，KB单位，自行显示易读的容量信息
   -s 列出总量，不列出每个个别的目录容量
   -k  以KB为单位显示容量
   -m 以MB为单位显示容量
```

```
fdisk		#磁盘分区操作工具
fdisk -l		#列出所有磁盘分区信息
```

---

## 4.VIM

**<u>vim是Linux系统下的标准编辑器,具有三种模式:命令模式、编辑模式和底行模式</u>**

![linux-senior-1-17](E:\Linux class\picture\linux-senior-1-17.png)

1）命令模式
vim [文件名]，进入命令模式

```
vim a.txt		#编辑a.txt文件，如果没有就新建a.txt文件
```

>命令模式下的操作有：
>【k 或 上箭头】向上移动一个字符
>【j 或 下箭头】向下移动一个字符
>【h 或 左箭头】向左移动一个字符
>【l 或 右箭头】向右移动一个字符
>注：hjkl在键盘上是连在一起的
>【gg】移动到文件第一行
>【G】移动到文件最后一行
>【nG】移动到文件第n行
>【0】数字0，移动到光标所在行的第一个字符
>【$】移动到光标所在行的最后一个字符
>【+】移动到非空格符的下一行
>【-】移动到非空格符的上一行
>【/string】从光标之下查找string字符串
>【?string】从光标之上查找string字符串
>【n】重复前一个搜寻操作，比如不停的查询string字符串
>【N】反向重复前一个搜寻操作，比如之前的操作是/string，向下查询字符串string，那么N就是向上查询string字符串
>【:n1,n2s/sring1/string2/g】n1行到n2行的内容中的sring1全部替换为sring2
>【:%s/sring1/string2/g】第一行到最后一行的内容中的sring1全部替换为sring2
>【:n1,n2s/sring1/string2/gc】n1行到n2行的内容中的sring1全部替换为sring2，在替换前提示字符给用户，确认是否替换
>【:%s/sring1/string2/gc】第一行到最后一行的内容中的sring1全部替换为sring2，在替换前提示字符给用户，确认是否替换
>【x】向后删除一个字符
>【X】向前删除一个字符
>【dd】删除光标所在的一整行
>【ndd】删除光标所在的向下n行（包含光标所在行）
>【yy】复制光标所在的一整行
>【nyy】复制光标所在的向下n行（包含光标所在行）
>【p】将复制的内容粘贴在光标的下一行
>【P】将复制的内容粘贴在光标的上一行
>【u】撤销上一个操作
>【Ctrl + r】重复上一个操作
>【.】小数点，重复上一个操作，比如连续删除、粘贴等
>下图为查找error字符串：
>![img](https://jn1.is.shanhe.com/chongyoulab/images/linux/linux-senior-1-18.png)
>下图为将文件中的所有error字符串替换为errortest字符串
>![img](https://jn1.is.shanhe.com/chongyoulab/images/linux/linux-senior-1-19.png)
>
>2）编辑模式
>【i】进入编辑模式，insert首字母的小写，从当前光标处输入
>【I】进入编辑模式，insert首字母的大写，从当前光标所在行的第一个非空格符处输入
>【a】进入编辑模式，从当前光标所在行的下一个字符处输入
>【A】进入编辑模式，从当前光标所在行的最后一个字符处输入
>【o】进入编辑模式，从当前光标下一行输入新的一行
>【O】进入编辑模式，从当前光标上一行输入新的一行
>【ESC】退出进入编辑模式，回到命令模式
>
>3）底行模式
>【:w】保存修改内容
>【:q】退出vim（用这个命令时，不能修改文件内容，否则，会提示是否修改）
>【:q!】不报错修改内容，强制退出
>【:wq】保存修改内容后退出
>【:wq!】保存修改内容后，强制退出
>【:set nu】显示行号
>【:set nonu】取消行号
>![img](https://jn1.is.shanhe.com/chongyoulab/images/linux/linux-senior-1-20.jpg)
>
>![img](https://jn1.is.shanhe.com/chongyoulab/images/linux/linux-senior-1-21.jpg)

---

## 5.GETDIT

**<u>getdit是Linux桌面模式下的编辑器.打开方式:进入桌面模式，点击Applications——> Accessories——> gedit，打开gedit编辑器</u>**

#### 1.操作

1）编辑喜好设置
单击Edit——>Preferences
设置行号，字体形式、大小、颜色

2）设置语法高亮
单击View——>Highlight Mode
选择对应的语言

3）保存文件
编辑文件后，单击File——>Save保存文件
或者，单击File——>Save As另存为其他文件
