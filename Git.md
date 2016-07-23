## 安装Git

1、Git下载地址：[https://git-scm.com/download/](https://git-scm.com/download/)

	$ sudo apt-get install git

2、[Git-Book-Online](https://git-scm.com/book/zh/v2)

3、Git图片原理解析

![](http://s7.sinaimg.cn/middle/001VHTmCzy707anPSwC16&amp;690)

## Git文件的三种状态

 Git 有三种状态，你的文件可能处于其中之一：已提交（committed,对应git commit命令）、已修改（modified）和已暂存（staged,对应git add命令）。 已提交表示数据已经安全的保存在本地数据库中。 已修改表示修改了文件，但还没保存到数据库中。 已暂存表示对一个已修改文件的当前版本做了标记，使之包含在下次提交的快照中。对应Git项目的三个工作区域的概念：Git 仓库(git commit)、工作目录以及暂存区域(git add)。

基本的 Git 工作流程如下：
1、在工作目录中修改文件。
2、暂存文件，将文件的快照放入暂存区域。
3、提交更新，找到暂存区域的文件，将快照永久性存储到 Git 仓库目录。

## Git命令

1、git配置

	$ git config -l
	$ git config --global user.name "Your Name"
	$ git config --global user.email "email@example.com"
	// 设置分支颜色
	$ git lg
	$ git config --global alias.lg "log --oneline --decorate --all --graph"

	//设置匹配模式
	$ git config --global push.default simple
	$ git config --global push.default matching

2、ssh key方式连接git

	$ ssh-keygen -t rsa -C "$your_email"
	$ cat ~/.ssh/id_rsa.pub

3、两种方式克隆远程版本库

	$ git clone 版本库地址
	$ git clone -o 指定远程主机名 版本库地址

	// 初始化项目，添加远程主机
	$ git init
	$ git remote add 远程主机(默认origin) 版本库地址 

4、分支

	$ git branch        // 查看分支
	$ git branch 分支名     // 创建分支
	$ git checkout 分支名    // 切换分支
	$ git checkout -b 分支名    // 创建并切换分支

5、在分支上常用命令
	
	$ git status   	  // 查询文件状态 	
	$ git log   //查看历史提交

	// 将当前分支的信息提交到暂存区
	$ git add 文件	  // 跟踪文件，提交文件到暂缓区
	$ git rm 文件	   // 移除文件
	$ git reset HEAD 文件  //从暂存区移除文件
	$ git commit -m "message"   // 提交文件到版本库
	$ git diff 文件  //只显示尚未暂存的改动，而不是自上次提交以来所做的所有改动
	$ git diff --cached
	$ git diff --staged
	$ git mv file_from file_to //移动文件

	//合并分支到当前分支.git merge与git rebase区别：通过git lg查看历史时是否只保留一条分支
	$ git merge 分支名
	$ git rebase 分支名

	$ git branch  //显示所有分支
	//删除本地分支，-d选项只能删除合并过的分支，未合并分支无法删除，想强制删除分支，可以使用-D选项
	$ git branch –d 分支名

	//在rebase过程中遇到冲突，git会停止rebase并让你解决冲突，解决完后通过git add提交修改后的内容再继续执行rebase
	$ git rebase -continue

	//终止rebase行动，让当前分支回到rebase开始前状态
	$ git rebase –abort

6、同步远程数据与本地数据

	//推送本地分支到远程指定分支
	$ git push origin <指定远程分支>
	$ git push origin –delete <远程分支名>


	//取回远程分支更新,与本地指定分支合并，等同于先做git fetch，再做git merge操作。后面参数都省略表示取回与本地当前分支同名的远程分支数据。如果希望合并采用git rebase模式，可以加—rebase选项
	$ git pull
	$ git pull –-rebase

	//跟踪远程分支
	$ git checkout -b [branch] [remotename]/[branch]

7、忽略文件(.gitignore)

文件 .gitignore 的格式规范如下：

> 所有空行或者以 ＃ 开头的行都会被 Git 忽略。

> 可以使用标准的 glob 模式匹配。

> 匹配模式可以以（/）开头防止递归。

> 匹配模式可以以（/）结尾指定目录。

> 要忽略指定模式以外的文件或目录，可以在模式前加上惊叹号（!）取反。




		


