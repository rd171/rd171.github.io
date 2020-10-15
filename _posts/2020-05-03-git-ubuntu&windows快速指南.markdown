---
layout: post
title:  "git-ubuntu&windows快速指南"
date:   2020-05-03 19:00:00 +0200
categories: git
---
### 1、全局配置
配置全局账户和邮箱
```
git config --global user.name 'yanf'
git config --global user.email 'yanf@de.com'
```
### 2、查看全局配置
```
git config --list
```
### 3、命令别名配置
将git status配置为git st
```
git config --global alias.st status
```
### 4、查看仓库的配置信息
进入仓库所在目录，打开.git文件夹下的config文件，或者输入如下命令:
```
cat .git/config
```

### 5、取代码
取master
```
git clone http://192.168.1.251:20200/chenzm/bm-7i.git
```
取分支   
```
git clone -b 分支名 http://192.168.1.251:20200/chenzm/bm-7i.git
```
取标签
```
git clone -b 标签名 http://192.168.1.251:20200/chenzm/bm-7i.git
```
### 6、打标签
```
git tag -a 标签名 -m '日志'
git push --tag
```

### 7、日志
```
git log
```
得到如下日志
```
commit 14550575f5d545f3fb016cffe197c65f303a23d1 (HEAD -> master, origin/master, origin/HEAD)
Author: yanf <yanf@de.com>
Date:   Sun May 3 11:39:14 2020 +0800

    1、增加pdf接口

commit 33117bcbe4e920849cd5c2c06e843f5ba4649c23
Author: yanf <yanf@de.com>
Date:   Sun May 3 11:14:48 2020 +0800

    1、集成pdf功能
```

每条日志都有一个唯一ID，我们可以通过这个ID来追加tag，见如下命令：   
```
git tag -a 标签名 33117bcbe4e920849cd5c2c06e843f5ba4649c23 -m '日志'
git push --tag
```
如果日志太多，只想看特定内容的日志，我们可以使用如下命令进行过滤，例如只看包含fix bug的日志（--pretty=oneline表示每一行显示一个提交，grep表示检索文本）
```
git log --pretty=oneline | grep fix
```

### 8、查看文件状态
![image](/img/2020-05-03-git-ubuntu&windows快速指南/status.jpg "image")  
git有三种文件状态：untracked（未跟踪）、unmodified（已跟踪未修改）、modified（已跟踪并修改）、staged（已跟踪已修改已暂存，通过git add命令提交至暂存区），通过以下命令可以查看：
```
git status
```
### 9、查看文件修改
```
git diff
```
diff命令默认是查看未提交至暂存区的变化，查看提交至暂存区的变化，可使用如下命令：
```
git diff -- staged
```

### 10、提交文件
工作日志应以如下格式进行提交，方便查询和生成changelog:   
type(scope):subject  

项目|说明   
-|-  
type|变更类型，例如：feat(新功能)，fix（修复bug），style（格式调整），refactor（代码重构），chore（项目构建）  
scope|变更范围，例如：电压测量模块  
subject|变更的具体内容，例如：定向修正10Hz信号幅度  

完整示例如下：
```
git commit -m 'fix(VolMeasure):定向修正10Hz信号幅度'
```

### 11、撤销提交
先用获得日志，得到要撤销位置对应的日志ID
```
git log
```
得到如下日志
```
commit 14550575f5d545f3fb016cffe197c65f303a23d1 (HEAD -> master, origin/master, origin/HEAD)
Author: yanf <yanf@de.com>
Date:   Sun May 3 11:39:14 2020 +0800

    1、增加pdf接口

commit 33117bcbe4e920849cd5c2c06e843f5ba4649c23
Author: yanf <yanf@de.com>
Date:   Sun May 3 11:14:48 2020 +0800

    1、集成pdf功能
```
撤销命令,会撤销指定日志之后的所有提交
```
git reset --hard 33117bcbe4e920849cd5c2c06e843f5ba4649c23
git push
```

### 12、解决代码冲突
代码冲突是因为staged状态的文件冲突，解决方法可以reset冲掉staged区的文件，非staged区的文件不受影响
```
git reset --hard
git pull
```

### 13、更新代码提示unmerged
手动解决代码冲突后，用add命令添加到staged，然后提交,例如code/BM/xxx/yyy.cpp: unmerged(6ed7ff345b033d676d0f493b4ce90a6db1fb7cf5)
```
git add yyy.cpp
git commit -m 'merge'
git push
```

### 14、取删除的代码
```
git reset DevOps 文件名
git checkout 文件名
```

### 15、安装git
![image](/img/2020-05-03-git-ubuntu&windows快速指南/git&tgit.jpg "image")
windows下载file:///C:/Users/Kevin/Downloads/TortoiseGit-2.10.0.2-64bit.msi并安装
ubuntu执行如下命令
```
apt install git
```

### 16、修改日志
1）、将当前代码rebase到一个分支，2表示最近2次提交   
```
git rebase -i HEAD~2
```
2）、在编辑界面中输入i，进入编辑，将pick该为edit，表示要修改   
3）、编辑完后在英文输入法下按ESC键，然后输入:wq   
4）、本地提交修改   
```
git commit --amend
```
5）、将分支还原   
```
git rebase --continue
```
6）提交到服务器   
```
git push
```

### git命令行窗口
windows右键菜单中选择Git Bash Here   
Ubuntu右键

接口人   
查看自己账户信息
三种访问仓库的方法   
从cvs、svn转换过来的痛点
查看版本记录
版本、标签、命名规则
拉分支
合并分支
打标签:完整功能提交后打tag，不像svn每次提交都有版本号
解决冲突
取删除文件
clone与check out 区别
origin与master区别
git add作用
git必知必会的重要命令
版本申请流程
