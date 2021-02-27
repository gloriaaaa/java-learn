# Git关联步骤
- 进入项目目录
```
git init
git add filename 或 git add .
git commmit -m "add xxx file" 
git status
```
- 创建仓库并关联
```
git remote add origin git@github.com:gloriaaaa/workdiary.git
git push -u origin master 
```
- 下次`add` `commit`　然后　`git push origin master`
- 删除文件
　`git rm -r --cached 文件夹名`
　`git rm --cached 文件夹名`