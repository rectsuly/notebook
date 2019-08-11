## Git常用命令

```
1 查看历史记录：
git log

git log --pretty=oneline

git log --oneline

git log --graph

git reflog

2 版本前进后退：

基于索引值操作：
git reset --hard a6ace91

使用^符号：只能后退
git reset --hard HEAD^
注：一个^表示后退一步，n个表示后退n步

使用~符号：只能后退
git reset --hard HEAD~n
注：表示后退n步

3 reset命令的三个参数对比

--soft参数：仅仅在本地库移动HEAD指针
--mixed参数：在本地库移动HEAD指针；重置暂存区
--hard参数：在本地库移动HEAD指针；重置暂存区；重置工作区

4 删除文件并找回

前提：删除前，文件存在时的状态提交到了本地库。
git reset --hard  [指针位置]
删除操作已经提交到本地库：指针位置指向历史记录
删除操作尚未提交到本地库：指针位置指向HEAD

5 比较文件差异

将工作区中的文件和暂存区进行比较：
git diff [文件名]

将工作区中的文件和本地库历史记录进行比较：
git diff [本地库中历史版本] [文件名]

不带文件名比较多个文件

6 分支操作

创建分支：
git branch [分支名]

创建并切换到分支：
git checkout -b [分支名] = git branch [分支名] + git checkout [分支名]

查看分支：
git branch -v

删除分支：
git branch -d [分支名]

丢弃一个没有被合并过的分支：
git branch -D [分支名]

切换分支：
git checkout [分支名]

合并分支：
第一步：切换到接受修改的分支（被合并，增加新内容）
git checkout [被合并分支名]、
第二步：执行merge命令
git merge [有新内容分支名]

解决冲突：
第一步：编辑文件，删除特殊符号
第二步：把文件修改到满意的程度，保存退出
第三步：git add [文件名]
第四步：git commit -m "日志信息"
注意：此时commit一定不能带具体文件名

7 克隆

git clone [远程地址]
效果：
完整地把远程库下载到本地
创建origin远程地址别名
初始化本地库

查看远程库信息：
git remote 
git remote -v

8 拉取

pull=fetch + merge
git fetch [远程库地址别名] [远程分支名]
git merge [远程库地址别名/远程分支名]


9 SSH登录

进入当前用户的家目录：
cd ~
删除.ssh目录
rm -rvf .ssh
运行命令生成.ssh密钥目录
ssh-keygen -t rsa -C xxx@xx.com
进入.ssh目录查看文件列表
cd .ssh
ls -lF
查看id_rsa.pub文件内容
cat id_rsa.pub
复制id_rsa.pub文件内容，登录GitHub，点击用户头像->Settings->SSH and GPGkeys
New SSH Key
输出复制的密钥信息，回到Git bash创建远程地址别名：
git remote add origin_ssh git@github.com:xxx/xx.git
推送文件进行测试

10 储存工作现场

git stash
git stash list

恢复：
git stash apply + git stash drop
git stash pop

恢复指定的stash
git stash apply stash@{0}

11 标签

打标签
git tag v1.0 f52c445
git tag -a v0.1 -m "version 0.1 released" 10de453

查看标签
git tag 
git show v0.9

删除标签：
git tag -d v0.1

推送标签：
git push origin v1.0
git push origin --tags

删除远程标签：
git tag -d v0.9
git push origin :refs/tags/v0.9

12 忽略文件

https://github.com/github/gitignore

强制添加：
git add -f [文件名]

检查规则：
git check-ignore -v [文件名]

配置别名：
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.unstage 'reset HEAD'
git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"
```

