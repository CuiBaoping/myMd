# 参考网址

[Git Bash参考网址](https://www.open-open.com/lib/view/open1414396787325.html)
[GitHub Desktop官网](https://docs.github.com/cn/desktop)
[使用GitHub Desktop管理GitLib](https://blog.csdn.net/towrabbit/article/details/95224578)
[GitHbu国内加速](https://www.zhihu.com/question/38192507)

# 下载并安装git
[下载地址](http://git-scm.com/downloads)
1，安装：使用默认安装
2，运行"Git Bash"
3，设置用户名和邮箱
​     git config --global user.name "username"
​     git config --global user.email "useremail"

# 忽略上传文件".gitignroe"，内容可使用通配符"*"
 1，如忽略QT编译文件目录使用"Build-*"
 2，如忽略QT"user"文件使用"*.user*"
注意：这个文件只作用于它所在目录，若子目录需要，请在子目录中创建这个文件

# 已有文件首次同步到GitHub或者GitLab
1，运行"Git Bash"
2，使用"cd"命令进入待上传目录
     注意：Windows盘符为"C:","D:"等，对应Git Bash为"/C/","/D/"
3，输入"git init"创建代码仓库
4，添加目录文件到暂存"git add ."
     添加一个文件到暂存"git add readme.txt"
     注意：添加目录中所有文件到暂存时间比较长，请耐心等待
5，在GitHub或者GitLab中创建工程，并复制工程路径：
     如："https://git.cdhn.tk/cuibaoping/tltp.git"
6，建立关联
     git remote add origin https://git.cdhn.tk/cuibaoping/tltp.git
7，推送到远程库（第一次加"-u"选项）
     git push -u origin master

# 从远程拉取到本地
如："https://git.cdhn.tk/cuibaoping/tltp.git"
1，运行"Git Bash"
2，使用"cd"命令进入待保存项目的目录
3，拉取项目
     git clone https://git.cdhn.tk/cuibaoping/tltp.git
     注意：在本地中项目会在"./tltp"目录中
4，重新定向远程库
     git remote set-url origin http://192.168.100.235:9797/john/git_test.git
5，查看远程库
     git remote -v
6，新建远程库
     git remote add http://192.168.100.235:9797/john/git_test.git

# 多人协作
1，推送本地到远程库：git push 或者 git push origin xxx
2，失败提示合并失败，同步远程库到本地：git pull
3，有冲突发生，在本地生成临时分支：git pull --rebase origin xxx 
4，解决冲突，并合并临时分支到本分支 git merage xxx
5，再次提交远程库：git push

# 日常使用
1，添加文档
     git add xxx.xxx
2，提交修改
     git commit -m "本次修改描述"
3，查看状态
     git status
4，显示日志
     git log
     git log –oneline		每行显示一个日志
5，回退版本
     git reset --hard HEAD^	回退前1版本
     git reset --hard HEAD^^	回退前2版本
     git reset --hard HEAD~100	回退前100版本
6，获取版本信息
     git reflog
7，撤销修改
     git restore xxx.xxx
     git checkout -- xxx.xxx
8，推送到远程库
     git push origin master
9，创建分支
     git branch dev		创建dev分支
     git checkout -b dev	创建并切换到dev分支
     git checkout -b dev  origin/dev	创建、拉取远程库并切换到dev分支
10，查看当前分支
     git branch	查看分支
     git branch -r	查看远程库分支
     git branch -a	查看本地及远程库分支
     git checkout dev	切换到dev分支
11，合并分支到当前分支
     git checkout master	切换到master主分支
     git merge dev		合并dev分支到master主分支
12，删除分支
     git branch -d dev		删除dev分支
13，隐藏当前工作现场
     git stash
14，查看隐藏的工作现场
     git stash list
15，恢复工作现场
     git stash apply	恢复现场 需要用 git stash drop删除stash
     git stash pop	恢复现场并删除stash
16，查看远程库版本
     git remote	查看远程库信息
     git remote -v	查看远程库详细信息
17，推送到分支
     git push			推送当前分支到远程库
     git push --set-upstream origin dev	关联远程库和本地的dev分支并推送
     git push origin dev		推送到dev分支
     git push origin mastor		推送到mastor主分支
18，抓取分支
     git pull
     git pull -–rebase origin master	同步远程库到本地mastor主分支上
19，删除远程库分支
      git push origin --delete branch-name
20，关联本地分支与远程库分支
     git fetch origin 远程分支xxx:本地分支xxx





