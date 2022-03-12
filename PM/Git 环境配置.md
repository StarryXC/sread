```
Git # GitHub
命令行
git
	--help
	--version

git init # 初始化仓库

git branch # 查看本地分支
	-a

git clone <url> # scheme: http https ssh git
	-b <branch> # 指定分支拉取

git pull # 更新本地分支
	origin <branch> # 拉取指定分支

git push # 推送本地仓库到远程仓库
	-u origin master

git fetch

git status



git add 添加文件到代码库
git add origin 添加库源
git add origin <branch> 默认 master
git add origin url 远程url

git commit 提交文件到代码库
git commit -m "update" 提交日志
git commit -am 添加当前所有文件并提交

git config
git config --system http.sslcainfo D:\\Programs\\Git\\mingw32\\ssl\\certs\\ca-bundle.crt
git config --global user.email "czwxiaoliang@163.com"
git config --global user.name "czwxiaoliang"

.gitconfig
[user]
	email = czwxiaoliang@163.com
	name = chengzhiwei



git remote 关联远程库
git remote -v 显示远程库版本

git merge 合并分支
git merge origin/master --allow-unrelated-histories 解决冲突

ssh-keygen # 密钥生成器

.gitignore
/build	目录
/name/
*.ext
/name/name.ext
/* 所有文件
name/ 根目录 子目录
# 注释

通配符
/ 斜杠 目录
* 星号 匹配多个字符
? 问号 匹配单个字符
[] 方括号 单字符匹配列表
! 不忽略文件 跟踪文件


```

> Thinking

```

```

> Memory

```

```

