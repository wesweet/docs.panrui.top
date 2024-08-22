<!--
 * @Description: git使用规范
 * @Author: panrui
 * @Date: 2023-04-25 08:57:17
 * @LastEditTime: 2024-04-29 14:28:47
 * @LastEditors: prui
 * 不忘初心,不负梦想
-->

# GIT

- [学习教程](https://learngitbranching.js.org/?locale=zh_CN)
- [提交格式](https://github.com/kazupon/git-commit-message-convention)

## Git 代码提交

```
<type>(<scope>): <short summary>
```

| type | build        | ci                 | docs     | feat   | fix      | perf     | refactor | test |
| ---- | ------------ | ------------------ | -------- | ------ | -------- | -------- | -------- | ---- |
| 描述 | 修改项目依赖 | 更改配置文件和脚本 | 文档修改 | 新功能 | 修复 bug | 性能优化 | 代码迭代 | 测试 |

## Git 操作技巧

#### 基本操作

```js
// 初始化仓库
git init
// 添加文件
git add <file>
// 提交文件
git commit -m "message"
// 查看修改状态
git status
// 查看文件修改的地方
git diff <file>
// 显示当前分支日志
git log | git log --pretty=oneline(简洁版--版本号和注释)
// 版本回退(当使用id的时候可以回退过去,也可以返回到未来)
git reset --hard HEAD~(number) | 回退
git reset --hard 版本id |返回到这个版本(如果这个版本id在当前版本id之后就属于回到未来)
// 查看文件内容
cat <file>
// 记录git使用的命令历史
git reflog
// 撤销修改(文件修改了,但是还没有放到暂存区,此时和版本库一致;放到暂存区以后又发生修改,回到添加到暂存区后的状态)
git checkout --<file>
// 将暂存区的修改撤销掉,重新放回工作区
git reset HEAD <file>
// 用版本库里的版本替换工作区的版本
git checkout --<file>
// 删除文件
git rm <file>
// 取消管理远程仓库
git remote remove origin
//推送代码
git push origin master
//克隆远程代码
git clone git@github.com:michaelliao/gitskills.git
// 查看远程仓库地址
git remote -v
// 储藏
git stash save "描述"
// 储藏历史
git stash list
// 还原储藏
git stash apply stash@{0}
// 创建ssh秘钥
ssh-keygen -t rsa -C "youremail@example.com"
// 默认秘钥地址 id_rsa.pub公钥 id_rsa私钥
// 添加远程仓库
git remote add origin git@github.com:michaelliao/learngit.git
// 如果本地已经有仓库，再关联远程仓库，可能会出现合并失败
// (refusing to merge unrelated histories) 拒绝合并不相关的历史
// 解决办法：
git pull origin master --allow-unrelated-histories
// 取消冲突合并
git merge --abort
```

#### 分支管理

```js
// 创建并切换分支
git checkout -b dev ==  git branch dev +  git checkout dev
// 创建分支
git branch dev
// 切换分支
git checkout dev
// 查看分支
git branch
// 合并分支
git merge dev
// (如果害怕合并失败,可以现在当前开发分支在切一个分支出来,然后合并到master,然后解决冲突看看功能是否完全)
// 如果成功就可以切回去进行合并
// 删除分支
git branch -d dev
// 强行删除分支
git branch -D dev
// 删除远程分支
git push origin --delete dev

// 检出远程分支到本地分支
git fetch origin dev1.14.0:dev1.14.0
git fetch origin dev 检出分支到本地
git checkout -b release/alpha-1 origin/release/alpha-1
```

## 配置与修改用户名和邮箱

```js
// --global表示此台机器上的所有Git仓库都会使用这个配置
git config --global user.name "Your Name"
git config --global user.email "email@example.com"

// 查看git配置
git config -l
git config --global --list
git config --local -l
git config --system -l
```

## Git .gitignore 无效

```js
git rm -r –cached .
git add .
git commit -m 'update .gitignore'
```

最后更新时间：2024-8-22 14:11:15
