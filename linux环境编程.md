# 文件

shell 与linux内核交互的软件。可以在其中输入命令

shell命令分为内部和外部命令，内部命令是由shell实现的，外部命令是一个可执行程序，shell 会使用exec函数来启动这个可执行程序。

type命令：可以通过type命令来判断一个命令是内部还是外部命令。

history命令：可以查看用户输入命令的历史记录。

PATH变量：shell执行外部命令时他是从哪里查找这个可执行程序的呢？shell会根据它的PATH变量中存储的地址来查找用户输入的命令。如果在这些目录下没有找到用户输入的命令，就会报错：×××不是内部或外部命令。

##shell快捷键

ctrl + p 显示上一条命令（previous）

ctrl + n 显示下一条命令（next）

ctrl + b 光标往回移动（back）

ctrl + f 光标向右移动（forword）

ctrl + a 光标移动到开头 （ahead）

ctrl + e 光标移动到结尾 （end）

## linux系统目录结构

/ 
 |-bin/
 |-dev/
 |-etc/
 |-home/
 |-lib/
 |-media/
 |-mnt/
 |-root/
 |-usr/
 	 |-


# 打包压缩和常用服务的搭建

# vim和函数库

## vim



## gcc



## 静态库



## 动态库



# makefile



# 文件io函数



文件操作函数



目录操作函数

