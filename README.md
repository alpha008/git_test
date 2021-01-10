# pro_go
study go

AAA
1.新建分支并推送到远程
git checkout -b slave 在本地新建分支 并不会推送到远程

git push orgin slave  会将本地分支推送到远程
主分支领先
1.新建分支并推送到远程
 新建分支只是在本地存在，需要推送到远程，才会被所有人看到
git checkout -b slave
git push origin slave
git push --set-upstream origin slave
设置远程关联的分支

2.删除分支并推送到远程
 删除分支只是在本地存在，需要推送到远程，才会被所有人看到 
 git branch -d slave
 git push origin -d slave

3.删除stash中的内容
删除 stash 的内容 ,感觉整个世界都清净了
其实就这么几行命令:
git stash list //查看stash 列表
如果得到这结果说明你的stash 是没有东西的

 删除一个
 git stash drop stash@{0}  
 删除所有
 git stash clear

4.本地分支可以随便修改，最终在确认就好了

本地分支开发，先要与master分支同步，解决冲突，然后在merge到远程分支

自己的分支先提交自己的分支，提交不同的分支是不允许的会出现不匹配
删除本地分支并同步到远程

5.查看远程关联的分支
git branch -vv

6. 当将别人的分支merge到本地后，如果想提交那么就需要push到远程


7.test slave分支先保存
在A 分支 git stash 然后在切换分支，然后执行git stash pop会把当前修改带到新的分支


8.slave test
如果你对一份代码随便搞又不影响你正常开发那么你最好新建一个分支，然后随便加注释代码
然后在及时更新master代码，那么就不会有影响

9.main分支
add
当执行add后后悔了想回退那么就执行
git reset +filename

10.当你执行git add 后在修改代码会出现下列情况
ubuntu@VM-0-17-ubuntu:~/pro_go$ git status 
On branch main
Your branch is up to date with 'origin/main'.

Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	modified:   README.md

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   README.md

11.当执行git add 后添加到提交区域
后悔了，那么执行git reset filename可以回退回来


12.当执行commit后想回退怎么办
1c10cab (HEAD -> main) HEAD@{0}: commit: add commit
7867478 (origin/main, origin/HEAD) HEAD@{1}: commit: add reset info
ubuntu@VM-0-17-ubuntu:~/pro_go$ git reflog 
1c10cab (HEAD -> main) HEAD@{0}: commit: add commit
7867478 (origin/main, origin/HEAD) HEAD@{1}: commit: add reset info
ubuntu@VM-0-17-ubuntu:~/pro_go$ git reset 7867478 --soft 
可以执行软回退1c10cab 会回退到这一次的记录，此次记录包含了你当时所做的修改
如果是--hard那么就找不回来了
13.
git commit -m "add info "
git commit --amend 在没有push之前可以修改提交说明

14.清除本地修改
git checkout -- filename
git chekout .


15.删除远程文件
git add delname


16.查看某一次的提交记录
git log -p 337c18a24ed481bbb3e96ec57fe77e489e9c6d92


commit 337c18a24ed481bbb3e96ec57fe77e489e9c6d92
Author: alpha008 <zjxlove2017@163.com>
Date:   Sat Jan 9 23:45:42 2021 +0800

    add dy

commit 0cb3c65e3184533f24ae2adf6614190725ddb7f1
Author: alpha008 <zjxlove2017@163.com>
Date:   Sat Jan 9 23:45:22 2021 +0800

    del local mod

commit 48a538c6eb6ef225dfc889d1fbae09570e523bb3
Author: alpha008 <zjxlove2017@163.com>
Date:   Sat Jan 9 23:41:33 2021 +0800

    add amend


17.回退代码
git reset 48a538c6eb6ef225dfc889d1fbae09570e523bb3 --soft 
git reset 48a538c6eb6ef225dfc889d1fbae09570e523bb3 --soft 

<<<<<<< HEAD
18.git revert


19.当你从远程分支拉取代码的时候，如果两个分支同时修改了这份代码，那么就会出现冲突
那么保留其中一个就好了，解决冲突后要与那个分支merge这样以后才不会冲突

当你拉取远程分支产生冲突的时候先将本地代码git add | git commit 
然后执行git pull
这样在修改代码就好了

9.test


=======
18.想回退到某一次提交

      原理： git revert是用于“反做”某一个版本，以达到撤销该版本的修改的目的。比如，我们commit了三个版本（版本一、版本二、 版本三），
      突然发现版本二不行（如：有bug），想要撤销版本二，
      但又不想影响撤销版本三的提交，就可以用 git revert 命令来反做版本二，生成新的版本四，这个版本四里会保留版本三的东西，但撤销了版本二的东西。

      1.先查询记录
      ubuntu@VM-0-17-ubuntu:~/pro_go$ git log
      commit f9fd93f2c135159c3bad421f225ffe6ce472b29b (HEAD -> main, origin/main, origin/HEAD)
      Author: alpha008 <zjxlove2017@163.com>
      Date:   Sun Jan 10 00:07:01 2021 +0800

          add3

      commit cd23c819ee587f8df159c11caa479118b549a88a
      Author: alpha008 <zjxlove2017@163.com>
      Date:   Sun Jan 10 00:06:32 2021 +0800

          add 2

      commit 1f54a32c1bb12aca71a3c187d8965d520d8d603d
      Author: alpha008 <zjxlove2017@163.com>
      Date:   Sun Jan 10 00:06:08 2021 +0800

          add1
      2.执行下列命令
      git revert -n 8b89621019c9adc6fc4d242cd41daeb13aeb9861
      git commit -m "revert add text.txt"
      ubuntu@VM-0-17-ubuntu:~/pro_go$ git revert -n cd23c819ee587f8df159c11caa479118b549a88a
      ubuntu@VM-0-17-ubuntu:~/pro_go$ git commit -m "revert del add 2"
      [main a6dc379] revert del add 2
      1 file changed, 0 insertions(+), 0 deletions(-)
      delete mode 100644 add2
      3.提交代码
      ubuntu@VM-0-17-ubuntu:~/pro_go$ git push
      4.查看记录
      ubuntu@VM-0-17-ubuntu:~/pro_go$ ls
      add1  add3  README.md


19.合并多次提交记录
git rebase -i HEAD~2
按下键盘i进入编辑模式，要保留的记录使用pick，
其他的改为squash,按Esc退出编辑模式，:wq 保存并退出
选择你要合并的记录的上一个，然后执行下面命令

git rebase -i commitId 
规则是第一个不能为squash
$ git push
To https://github.com/alpha008/pro_go.git
 ! [rejected]        main -> main (non-fast-forward)
error: failed to push some refs to 'https://github.com/alpha008/pro_go.git'
hint: Updates were rejected because the tip of your current branch is behind
hint: its remote counterpart. Integrate the remote changes (e.g.
hint: 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.

使用git push -f

20.加入要将某一个分支的某一次提交合并到另外一个分支
例如要将A分支的一个commit合并到B分支：
首先切换到A分支
git checkout A
git log
找出要合并的commit ID :
例如
325d41
然后切换到B分支上
git checkout B
git cherry-pick 325d41
然后就将A分支的某个commit合并到了B分支了