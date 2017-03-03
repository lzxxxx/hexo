---
title: git学习笔记
---

# git 
## git常用指令

- 克隆一个项目

```
	$ git clone 项目地址
```

- 进入你克隆的项目，安装项目所需依赖(有package.json的话)

```
	$ cd 克隆后的项目位置
	$ git npm install
```

- 查看分支

```
	$ git branch
```

- 查看当前分支

```
	$ git branch -v
```

- 创建分支

```
	$ git branch 分支名
```

- 删除分支

```
	$ git branch -d 分支
```

- 创建并切换分支

```
	$ git checkout -b 分支名
```

- 切换分支

```
	$ git checkout 分支名
```

- 查看当前分支的所有文件

```
	$ ls -a
```

- 查看远程分支有哪些

```
	$ git branch -a
```

- 例如将本地test分支推送到远程服务器,此命令会创建新的分支，如果已存在test，可省略

```
	$ git push origin test
```

- 上传到远程服务器

```
	$ git push
	
	// 下边是报错信息（因为提交到分支需要给出--set-upstream origin <分支名>）
	fatal: The current branch test has no upstream branch.
	To push the current branch and set the remote as upstream, use
git push --set-upstream origin test

```

- 如下将提交推送到远程服务器

```
	$ git push --set-upstream origin test
```

- 更新项目

```
	$ git pull
```

- 添加文件到缓存区

```
	// 这是添加所有文件
	$ git add .
	// 添加单独文件
	$ git add 文件名
	// 添加文件夹
	$ git add 文件夹名
```

- 添加文件夹到本地仓库(先要进行上一步)

```
	$ git commit -m '添加描述(方便记住这次操作)'
```

- 查看修改状态

```
	$ git status
```

- $ 上传到远程仓库

```
	$ git push
```

- 删除文件夹

```
	// 删除本地文件夹后上传
	$ git rm -rf 文件名
	$ git add .
	$ git commit -m "描述"
	$ git push
	
	// 直接删除本地缓存后上传
	$ git rm -r --cached some-directory
	$ git commit -m "描述"
	$ git push
	
```

- 不想上传某些文件

```
	// 在当前分支的目录下创建一个 .gitignore.txt 文件
	// 在文件内写下不想上传的文件，例如:
	// hello.html
	// dir
```



