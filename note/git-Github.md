# 1. 版本控制的概念
-  本地版本控制系统 
-  集中版本控制系统 
-  分布式版本控制系统 
# 2.git基础概念
## 2.1Git中的三个区域
使用Git管理的项目，拥有三个区域，分别是工作区，暂存区，Git仓库。

| **分类** | **描述** |
| --- | --- |
| 工作区 | 就是你在电脑里能看到的目录 |
| 暂存区 | 英文叫 stage 或 index。一般存放在 .git 目录下的 index 文件（.git/index）中，所以我们把暂存区有时也叫作索引（index） |
| 版本库/Git库 | 工作区有一个隐藏目录 .git，这个不算工作区，而是 Git 的版本库。下面这个图展示了工作区、版本库中的暂存区和版本库之间的关系 |

## 2.2Git中的三种状态
| **状态** | **描述** |
| --- | --- |
| 已提交(committed) | 表示数据已经安全的保存在本地数据库中 |
| 已修改(modified) | 表示修改了文件，但是还没保存到数据库中 |
| 已暂存(staged) | 表示对一个已修改文件的当前版本做了标记，使之包含在下次提交的快照中 |

## 2.3Git基本的工作流程

![Snipaste_2023-03-23_13-18-00.png](https://cdn.nlark.com/yuque/0/2023/png/34913475/1679548695440-1f5ce7cc-1087-4131-a570-29be83135ff2.png#averageHue=%2380d870&clientId=uebdc776a-bcb5-4&from=ui&height=363&id=u48be1f6d&name=Snipaste_2023-03-23_13-18-00.png&originHeight=747&originWidth=1653&originalType=binary&ratio=1&rotation=0&showTitle=false&size=271804&status=done&style=none&taskId=u7ab1e242-54a7-475a-a4e1-f3089826838&title=&width=803)

---

# 3.git基本使用
## 3.1基本操作命令

- cd  #改变目录
- cd.. #回退到上一个目录，直接cd进入默认目录
- pwd  #显示当前所在的目录路径
- ls(ll) #都是列出当前目录中的所有文件，只不过ll(两个ll)列出的内容更为详细
- touch #新建一个文件 如 touch index.js 就会在当前目录下新建一个index.js文件
- rm #删除一个文件, rm index.js 就会把index.js文件删除
- mkdir #新建一个目录,就是新建一个文件夹
- rm -r #删除一个文件夹, rm -r src 删除src目录， 好像不能用通配符
- mv  #移动文件, mv index.html src index.html 是我们要移动的文件, src 是目标文件夹,当然, 这样写,必须保证文件和目标文件夹在同一目录下
- reset  #重新初始化终端/清屏
- history  #查看命令历史
- clear #清屏
- help  #帮助
- exit  #退出
## 3.2用户设置

- git config -- global user.name "xxx"
- git config --global user.email xxx
- git config --global --list （查看当前用户全局）
## 3.3Git中基本命令的使用

- **git init**
- **git add .**
- **git commit -m "提交信息"**
- **git commit -a -m "" （跳过暂存区）/ git commit -am "" （跳过暂存区）**
- **git status / git status -s[-short]**
- git checkout -- 文件名;（撤销）
- git reset HEAD 文件名;（取消暂存区文件）
- git rm -f 文件名;（移除Git仓库和工作区的文件）
- git rm --cached 文件名;（移除Git仓库文件，保留工作区文件）
- **git log;（查看历史提交）**
- git log  --pretty;
- git log -n --pretty;（前n条信息）
- 给git log --pretty=oneline
- **git reset --hard commitID;（版本切换）**
- git fetch upstream 更新本地版本
- git merge upstream/main 远程合并自己的代码
- clear
## 3.4使用Github创建维护远程仓库

- **git clone 地址;（远程仓库文件复制到本地仓库）**
- git push
- **git push -u origin 新分支名称;（本地分支上传到远程仓库）**
- **git pull;（远程仓库更新到本地工作区，会覆盖你的工作区）**

1. fetch （更新到本地仓库）
2. diff （本地仓库对比更新工作区）
## 3.5Git分支的基本使用

-  **git branch 查看你本地分支** 
-  git branch -a 查看本地远程分支 
-  **git branch 新分支名称** 
-  **girt branch -d[-D] 分支名; (删除本地分支，需要切换到别的分支，不能在自己的分支删除自己)** 
-  **git checkout 分支名称;（切换分支）** 
-  **git checkout -b 新分支名称;（分支快速创建和切换）** 
-  **git merge 分支名;（合并分支）** 
-  **git remote -v 查看本地仓库和哪些远程仓库有联系**
-  git remote add upatream 链接;  添加上游代码库链接 
-  git remote show origin;（查看远程仓库中所有分支列表） 
-  git checkout -b  .... origin/本地分支名 
-  **git push origin --delete 远程分支名; （删除远程分支）** 
# 4.Github
## 4.1.开源/闭源
开源是指不仅提供程序还提供程序的源代码
闭源是只提供程序，不提供源代码
## 4.2.开源许可协议

GPL/MIT
## 4.3.开源项托管平台

- Github
- Gitlab
- Gitee
# 5.Git与Github配合
## 5.1HTTPS
零配置，每次需要验证，复制给的3条代码，你的git仓库必须有文件，才能上传
## 5.2SSH
第一次需要配置，免登录加密数据传输
id_rsa（私钥文件，存放于客户端的电脑中即可）
id_rsa.pub（公钥文件，需要配置到Github中）
## 5.3生成SSH Key
ssh-keygen -t rsa -C "邮箱"，敲三次回车即可在C:\Users\用户名文件夹.ssh 生成id_rsa,id_rsa.pub
## 5.4配置SSH Key
用记事本打开id_rsa.pub文件，复制文本内容到Github上，New SSH key配置即可。
## 5.5验证是否配置成功
ssh -T [git@github.com](mailto:git@github.com)
## 5.6Clone与Download ZIP的区别
Download ZIP下载复制文件是没有.git文件的，所以不会有版本历史记录，下载的是当前最新的版本
![Snipaste_2023-03-23_13-39-23.png](https://cdn.nlark.com/yuque/0/2023/png/34913475/1679550022274-6e9ace16-f640-4b72-b8e8-868a042b4e0e.png#averageHue=%23191c21&clientId=ud3f4ea0f-571c-4&from=ui&id=u2460f650&name=Snipaste_2023-03-23_13-39-23.png&originHeight=401&originWidth=482&originalType=binary&ratio=1&rotation=0&showTitle=false&size=75496&status=done&style=none&taskId=u63e80525-5f7b-4672-a860-2c103bc0dea&title=)







