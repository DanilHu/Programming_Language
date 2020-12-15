# 基本操作
1. 状态查看操作
	`git status`：查看工作区、暂存区状态——属于哪一个分支，是否被提交
2. 添加文件到暂存区
	`git add [filename]`：将工作区“新建/修改”添加到暂存区
3. 提交
	`git commit -m "commit message" [filename]`：将暂存区的内容提交到本地库(在.git里面，与.git同级的是工作区)
	> 工作区是写代码的地方，暂存区是暂时存放改变的地方，本地库则是真正负责存储和版本控制的地方
4. 版本回退
	- 一般来讲退回的东西是不恢复的，如果想恢复就要设法弄到需要恢复版本的哈希值，可以通过历史命令查看`git reflog`
	**hard参数**
	在版本库里面移动HEAD指针，同时重置暂存区，同时重置工作区，这时就是所谓干净，三个区都同步
	`git reset --hard [num](只需要后面几个数字即可，能区分就行)`：可以到任何一个版本的状态
	`git reset --hard HEAD^`：只能后退版本，一个^退一步，两个^退两步
	`git reset -- hard HEAD~3`：后退n步，n由后面的n指定
	**soft参数**
	Does not touch the index file(暂存区) or the working tree(工作区) at all，仅仅只是移动HEAD指针                  
	**mixed参数**
	在版本库里面移动HEAD指针，同时重置暂存区
5. 使用镜像网站加快github访问速度`github.com.cnpmjs.org`
6. Git与远程仓库关联
	- 添加账号信息
	```
	$ git config --global user.name "Your Name"
	$ git config --global user.email "email@example.com"
	```
	- 在GitHub上创建远程库
	- 使用
	```
	git remote add origin URL
	git push -u origin master # 第一次提交
	git push origin master # 其他提交
	```
	
	
# 基本命令解释
1. `git log`：指示有多少个版本被提交了(版本号)前版本用HEAD指针说明，作者和时间以及每次提交的的message
  `git log`--oneline：由于上面显示的东西太多了，因此使用--oneline使得显示看起来更舒服
  `git reflog`：显示每一次的命令
2. 
