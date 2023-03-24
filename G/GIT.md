# GIT

[(Git 常用基本命令使用详细大全_git常用命令_坚强的小水滴的博客-CSDN博客](https://blog.csdn.net/qtiao/article/details/97783243)

> 总之先放一个链接                                  

## 基本指令

**git init**
  Git使用git init命令来初始化一个Git仓库，执行完git init命令后，会生成一个**.git**目录，该目录包含了资源数据，且只会在仓库的根目录生成

```
git init		#初始化一个git仓库/在当前目录创建仓库

git init newDir		#在指定的目录下生成仓库,newDir为仓库的路径，执行完成之后，会在newDir目录下生成一个.git目录
```



**git clone**

```
git clone <url> [directory]	  #url为git仓库地址，directory为本地目录，若没有输入directory，则在当前目录下生成仓库。
```

> git clone 时，可以用不同的协议，包括 ssh, git, https 等，其中最常用的是 ssh，因为速度较快，还可以配置公钥免输入密码，各种写法格式如下：
>
> git clone git@github.com/schacon/grit.git         --SSH协议
> git clone git://github.com/schacon/grit.git          --GIT协议
> git clone https://github.com/schacon/grit.git      --HTTPS协议



#### SSH配置

```
ssh-keygen -t rsa		#生成公钥和私钥

start ~		#公钥在.ssh里

cat ~/.ssh/id_rsa.pub	#查看公钥

ssh-keygen -t rsa -C "邮箱"		
#记得提前配置，然后进行3-4次确认
 确认秘钥的保存路径（如果不需要改路径则直接回车）；
 如果上一步置顶的保存路径下已经有秘钥文件，则需要确认是否覆盖（如果之前的秘钥
 不再需要则直接回车覆盖，如需要则手动拷贝到其他目录后再覆盖）；
 创建密码（如果不需要密码则直接回车）；
 确认密码。
 
clip < ~/.ssh/id_rsa.pub
#然后在github上面进入setting,点击SSH and GPG keys
 点击new SSH key,取个名字，粘贴，OK了
```



**git config**

```
git config --global user.name '你的用户名'
git config --global user.email '你的邮箱'
#通过git config来配置用户名和邮箱地址，将代码提交到远程仓库
```



**git add**

```
git add	.	#将文件添加到缓存,也可以指定某一类文件
栗子：
it add *.java
```



**git status**

```
git status		#查看相关文件的状态(显示已写入缓存与已修改但尚未写入缓存的改动的区别具体的详细信息)
```



**git fiff**

```
git diff		#查看更新的详细信息(只显示更新的状态)
```



**git commit**

```
git commit		#将缓存区内容添加到仓库中
		   -m	#在命令行中提供提交注释
		   -a	#跳过add这一步
```



**git reset HEAD**

```
git reset HEAD		#取消已缓存的内容,执行完之后，再使用commit提交时,文件不会被提交
```



**git rm**

```
git rm <file>		#将文件移除
	   -f			#强制删除（删除之前修改过并且已经放到暂存区域）
	   --cached		#从跟踪清单中删除（保留在当前工作目录）
	   –r *·		#递归删除
```



**git mv**

```
git mv test.txt newtest.txt		#移动或重命名一个文件、目录、软连接
```

---

## 分支管理

**git branch **

```
git branch		#查看分支，也可以创建分支，有参数时，git branch会列出在本地的分支；如果有参数时，git branch就会创建改参数的分支

git branch -d branchname	#删除分支
```



**git checkout **

```
git checkout branchname		#切换分支
			 -b				#创建新分支并立即切换到该分支下
```



**git merge **

```
git merge branchname		#将任意分支合并到到当前分支中
```

>**合并冲突**
>  合并时，Git 也会合并修改，如果在两个分支中同时修改了同一个文件，这时再合并，就可能会产生冲突。（总之就是不懂就问，我也没整过多少）

----

## 查看提交历史

**git log**

```
git log –oneline ：查看历史记录的简洁版本
		–graph ：查看历史中什么时候出现了分支、合并
		–reverse ：逆向显示所有日志
		–author ：查找指定用户的提交日志
		–since、–before、 --until、–after： 指定帅选日期
		–no-merges ：选项以隐藏合并提交
```

---

## 标签

**git tag -a vx.x**

```
git tag -a vx.x		#-a：创建带注解的标签（记录标签创建时间、创建者，禁止添加注解）
```



**git tag**

```
git tag		#查看标签
git tag -a <tagname> -m "某某标签"	#指定标签信息
git tag -s <tagname> -m "某某标签"	#PGP签名标签
```

---

## 远程仓库

**git remote add**

```
git remote add [别名] [远程仓库地址]
```



**git remote**

```
git remote		#查看当前有哪些远程仓库
```



**git fetch**

```
git fetch		#提取远程仓库的数据，有多个远程仓库时，加上别名
```

>该命令执行完后需要执行git merge 远程分支到你所在的分支。假设你配置好了一个远程仓库，并且你想要提取更新的数据，你可以首先执行 git fetch [alias] 告诉 Git 去获取它有你没有的数据，然后你可以执行 git merge [alias]/[branch] 以将服务器上的任何更新合并入你的当前分支



**git pull**

```
git pull		#从另一个存储库或本地分支获取并集成(整合)
git pull [options] [<repository> [<refspec>…]]
```



**git push**

```
git push [alias] [branch]		#推送新分支与数据到某个远端仓库
```



**git remote rm**

```
git remote rm [别名]		#删除远程仓库
```



