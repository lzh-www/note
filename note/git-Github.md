## Git

### 1. 版本控制的概念

- 本地版本控制系统

- 集中版本控制系统

- 分布式版本控制系统

### 2.git基础概念

##### 2.1Git中的三个区域

使用Git管理的项目，拥有三个区域，分别是工作区，暂存区，Git仓库。

##### 2.2Git中的三种状态

![](E:\Typora笔记\images\2022-08-20-19-37-16-image.png)

##### 2.3Git基本的工作流程

![image-20220827103154676](E:\Typora笔记\images\image-20220827103154676.png)

***

## Github

#### 1.开源/闭源

 开源是指不仅提供程序还提供程序的源代码

闭源是只提供程序，不提供源代码

#### 2.开源许可协议

GPL/MIT

#### 3.开源项托管平台

- Github
- Gitlab
- Gitee

#### 4. git基本命令使用

##### 4.1基本操作命令

- cd  #改变目录
- cd.. #回退到上一个目录，直接cd进入默认目录
- pwd  #显示当前所在的目录路径
- ls(ll) #都是列出当前目录中的所有文件，只不过ll(两个ll)列出的内容更为详细
- touch #新建一个文件 如 touch index.js 就会在当前目录下新建一个index.js文件
- rm #删除一个文件, rm index.js 就会把index.js文件删除
- mkdir #新建一个目录,就是新建一个文件夹
- rm -r #删除一个文件夹, rm -r src 删除src目录， 好像不能用通配符
- mv  #移动文件, mv index.html src index.html 是我们要移动的文件, src 是目标文件夹,当然, 这样写,必须保证文件和目标文件夹在同一目录下
- reset  #重新初始化终端/清屏
- history  #查看命令历史
- clear #清屏
- help  #帮助
- exit  #退出

##### 4.2用户设置

- git config -- global user.name ""
- git config --global user.email
- git config --global --list （查看当前用户全局）

##### 4.3Git中基本命令的使用

- <font color=red>**git init**</font>
- <font color=red>**git add .**</font>
- <font color=red>**git commit -m "提交信息"**</font>
- git commit -a -m "" （跳过暂存区）
- <font color=red>**git status / git status -s[-short]**</font>
- git checkout -- 文件名;（撤销）
- git reset HEAD 文件名;（取消暂存区文件）
- git rm -f 文件名;（移除Git仓库和工作区的文件）
- git rm --cached 文件名;（移除Git仓库文件，保留工作区文件）
- <font color=red>**git log  --pretty;（查看历史提交）**</font>
- git log -n --pretty;（前n条信息）
- 给git log --pretty=oneline
- <font color=red>**git reset --hard commitID;（版本切换）**</font>
- git fetch upstream 更新本地版本
- git merge upstream/main 远程合并自己的代码
- clear

##### 4.4使用Github创建维护远程仓库

- 配置Github的SSH访问
- 将本地仓库上传到Github
- <font color=red>**git clone 地址;（远程仓库文件复制到本地仓库）**</font>
- git push
- <font color=red>**git push -u origin 新分支名称;（本地分支上传到远程仓库）**</font>
- <font color=red>**git pull;（远程仓库更新到本地工作区，会覆盖你的工作区）**</font>

1. fetch （更新到本地仓库）
2. diff （本地仓库对比更新工作区）

##### 4.5Git分支的基本使用

- <font color=red>**git branch 查看你本地分支**</font>
- git branch -a 查看本地远程分支
- <font color=red>**git branch 新分支名称**</font>
- <font color=red>**girt branch -d[-D] 分支名; (删除本地分支，需要切换到别的分支，不能在自己的分支删除自己)**</font>
- <font color=red>**git checkout 分支名称;（切换分支）**</font>
- <font color=red>**git checkout -b 新分支名称;（分支快速创建和切换）**</font>
- <font color=red>**git merge 分支名;（合并分支）**</font>

- git remote -v
- git remote add upatream 链接;  添加上游代码库链接
- git remote show origin;（查看远程仓库中所有分支列表）
- git checkout -b  .... origin/本地分支名
- <font color=red>**git push origin --delete 远程分支名; （删除远程分支）**</font>

#### 5.Git本地仓库上传Github远程仓库

##### 5.1HTTPS

零配置，每次需要验证

复制给的3条代码

你的git仓库必须有文件，才能上传

##### 5.2SSH

第一次需要配置

免登录加密数据传输

id_rsa（私钥文件，存放于客户端的电脑中即可）

id_rsa.pub（公钥文件，需要配置到Github中）

##### 5.3生成SSH Key

ssh-keygen -t rsa -C "邮箱" 敲三次回车

即可在C:\Users\用户名文件夹\.ssh 生成id_rsa,id_rsa.pub

##### 5.4配置SSH Key

用记事本打开id_rsa.pub文件，复制文本内容

到Github上，New SSH key配置即可

##### 5.5验证是否配置成功

ssh -T git@github.com







