# Git

##### 初始化

```git
git init
```

##### 设置签名

```
git config user.name xxx
git config user.email xxx
git config --global user.name xxx
git config --global user.email xxx
```

##### 查看签名

```
项目级别
cd .git/
cat config 

系统级别
cat ~/.gitconfig
```

##### 设置忽略文件

```
新建：touch .gitignore
设置忽略文件：vim .gitignore
			#IDEA
			.idea
			*.iml\
			#eclipse
			.setting
			.project
			等等其他想要忽略的文件
```



##### 查看状态

```git
git status
```

##### 查看配置

```
git config --list
```



##### 工作区、暂存区、本地仓库

```
git add xxxfile
git commit xxxfile
git commit -m "注释说明内容" xxxfile
```

##### 查看日志

```
git log
git log --graph
git log  --pretty=oneline
git log  --oneline
git reflog
```

##### 日志太长

```
下一页：空格
上一页：b
退出查看：q
```



##### 切换版本

```
切换方式
--soft   只修改本地仓库指针，不会修改index和work tree
--mixed   修改本地仓库和index暂存区指针，不会修改work tree
--hard   修改本地仓库、index暂存区、work tree，三者更改到指定版本

哈希切换
git reset --切换方式  哈希值

~操作
git reset --切换方式 HEAD~n

异或操作
git reset --切换方式 HEAD^^^^^^^^^
```

##### 文件的四种状态

```
untracked：工作区状态
modify：修改状态
unmodified：未修改，工作区和本地仓库一致
staged：暂存区状态
```

##### (checkout)撤销工作区修改

```
文件已经在暂存区，又在工作区修改，
git checkout -- xxxfile
```

##### 撤销暂存区文件

```git
git rm --cached xxxfile
```

##### 观察暂存区和工作区difference

```
此命令必须要某文件add到暂存区后，再修改，即git status 时会看到此文件又有红又有绿
git diff xxxfile
```

##### 观察本地仓库和工作区的difference

```git
git diff HEAD xxxfile
```

##### 分支概述

```git
Production分支：产品发布，不能在此分支直接修改
master分支：其他分支合并而来，不能直接在此分支修改
develop分支：开发分支，feature分支、Hotfix分支等会合并到此，完成后进入release分支
feature分支：功能分支，完成后合并到develop分支
Hotfix分支：紧急bug分支，完成后合并到develop分支
release分支：测试分支，基于develop的分支，完成后合并到feature分支或者develop分支
```

##### 查看分支

```git
git branch -v
git branch
```

##### 增加分支

```
只创建：git branch xxxBranchName
创建并切换分支：git checkout -b xxxBranchName
```

##### 改名分支

```
git branch -m  oldBranchName  newBranchName
```

##### 切换分支

```
git checkout xxxBranchName
```

##### 合并分支

```
切换到接收分支的分支：
git checkout xxxMasterBranch
git merge  xxxTargerBranch
git rebase  xxxTargerBranch
```

##### 删除分支

```
git branch -d xxxBranchName
```

4312155840427

#### 与远程仓库交互

##### 使用ssh密钥方式

id_rsa.pub，即公钥可以给人看，可以在GitHub上粘贴

id_rsa，即私钥不可以外泄

生成ssh公钥和私钥

```
ssh-keygen   如果不对密钥使用密码的话，四次回车
ssh-keygen   如果使用密码的话，输入密码信息
ssh-keygen -t rsa –C “youremail@example.com”
```

![image-20210201154430129](C:\Users\Xgiao\AppData\Roaming\Typora\typora-user-images\image-20210201154430129.png)

![image-20210201154452644](C:\Users\Xgiao\AppData\Roaming\Typora\typora-user-images\image-20210201154452644.png)

![image-20210201154535393](C:\Users\Xgiao\AppData\Roaming\Typora\typora-user-images\image-20210201154535393.png)

##### 刷新密钥

```
ssh-keygen -p -f ~/.ssh/id_rsa
```

在GitHub自建库上面选择code->ssh->复制ssh链接

```
设置远程仓库别名：
git remote add 远程库别名 ssh链接地址
查看远程库：
git remote -v
删除远程库：
git remote rm 远程库别名
推送：
git push -u  远程库别名  本地分支名
```



##### 使用HTTPS方式

在GitHub自建库上面选择code->HTTPS->复制https链接

```
git push  https远程库别名  本地分支名
```

##### 克隆

```
整个项目克隆：
git clone  https://targetURL
分支克隆：
git clone -b 分支名 https://targetURL
```

##### pull和fetch

```
git pull origin master
等价于
git fetch origin master
git checkout master
git merge xxxBranch
```

###### clone和pull区别

```
clone是本地没有repository
pull是已经有repository，再从远程库拉取新的commit数据
```

## 报错

error:key  does  not  contain  a  section  :xx

原因：更改签名时没有使用user.name和user.email

