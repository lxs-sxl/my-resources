# Git常用命令	

| 命令                                                  | 作用                       |
| ----------------------------------------------------- | -------------------------- |
| git init                                              | 在当前目录初始化Git仓库    |
| git clone <url>                                       | 克隆远程仓库到本地         |
| git config --global user.name "你的名字"              | 全局配置用户名             |
| git config --global user.email "你的邮箱@example.com" | 全局配置邮箱               |
| git status                                            | 查看文件状态变更           |
| git add <文件名>                                      | 将指定文件添加至暂存区     |
| git add .                                             | 添加所有修改文件至暂存区   |
| git commit -m "提交说明"                              | 将暂存区代码提交至本地仓库 |
| git commit -am "提交说明"                             | 跳过暂存区直接提交修改     |
| git branch                                            | 查看本地分支               |
| git branch -a                                         | 查看所有分支（本地+远程）  |
| git branch <分支名>                                   | 创建新分支                 |
| git checkout <分支名>                                 | 切换分支                   |
| git merge <分支名>                                    | 合并目标分支到当前分支     |
| git remote add origin <url>                           | 关联远程仓库               |
| git push -u origin <分支名>                           | 推送分支至远程并关联       |
| git push origin <本地分支名>:<远程分支名>             | 自定义远程分支名推送       |
| git pull                                              | 拉取远程分支更新到本地     |