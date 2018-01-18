# git 常规操作
## 一.常见命令
###1. 安装git
git config --global user.name 'XXX'

git config --global user.email 'XXX'

###2. 常见CRT
>git init //初始化代码仓库
git add learngit.txt                               //把所有要提交的文件修改放到暂存区
git commit -m 'add a file'                      //把暂存区的所有内容提交到当前分支
git status                                            //查看工作区状态
git diff                                                //查看文件修改内容
git log                                                //查看提交历史
git log --pretty=oneline                       //单行显示
git reset --hard HEAD^　　 //回退到上一个版本，其中（HEAD^^(上上版本),HEAD~100(往上100个版本)）
commit id   //(版本号) 可回到指定版本
git reflog //查看历史命令
git diff HEAD -- <file>                                  //查看工作区和版本库里最新版本的区别
git checkout -- <file>                                   //用版本库的版本替换工作区的版本，无论是工作区的修改还是删除，都可以'一键还原'
git reset HEAD <file>                                   //把暂存区的修改撤销掉，重新放回工作区。
git rm <file>                                               //删除文件，若文件已提交到版本库，不用担心误删，但是只能恢复文件到最新版本

###3. 建立本地Git仓库和GitHub仓库之间的传输
>ssh-keygen -t rsa -C 'your email'                                                    //创建SSH Key
git remote add origin git@github.com:username/repostery.git          //关联本地仓库，远程库的名字为origin
git push -u origin master //第一次把当前分支master推送到远程，-u参数不但推送，而且将本地的分支和远程的分支关联起来
git push origin master                                                                  //把当前分支master推送到远程
git clone git@github.com:username/repostery.git                            //从远程库克隆一个到本地库

###4. 分支
>git checkout -b dev                                   //创建并切换分支
相当于git branch dev 和git checkout dev 
git branch                                                //查看当前分支，当前分支前有个*号
git branch <name>                                   //创建分支
git checkout <name>                                //切换分支
git merge <name>                                   //合并某个分支到当前分支
git branch -d <name>                               //删除分支
git log --graph                                          //查看分支合并图
git merge --no-ff -m 'message' dev            //禁用Fast forward合并dev分支
git stash                                                 //隐藏当前工作现场，等恢复后继续工作
git stash list                                            //查看stash记录
git stash apply                                         //仅恢复现场，不删除stash内容
git stash drop                                          //删除stash内容
git stash pop                                           //恢复现场的同时删除stash内容
git branch -D name                              //强行删除某个未合并的分支
git remote                                //查看远程仓库
git remote -v                                           //查看远程库详细信息
git pull                                                   //抓取远程提交
git checkout -b branch-name origin/branch-name                  //在本地创建和远程分支对应的分支
git branch --set-upstream branch-name origin/branch-name   //建立本地分支和远程分支的关联

###5. 其它
>git tag v1.0 //给当前分支最新的commit打标签
git tag -s &lt;tagname&gt; -m 'blabla'//可以用PGP签名标签
git tag//查看所有标签
git show v1.0//查看标签信息
git tag -d v0.1 //删除标签
git push origin &lt;tagname&gt; //推送某个标签到远程
git push origin --tags//推送所有尚未推送的本地标签


## 二.错误解决
 
>**问题一** 如果输入$ git remote add origin git@github.com:djqiang（github帐号名）/gitdemo（项目名）.git 
提示出错信息：fatal: remote origin already exists.
>解决办法如下：
>1. 先输入$ git remote rm origin
>2. 再输入$ git remote add origin git@github.com:djqiang/gitdemo.git 就不会报错了
>3. 如果输入$ git remote rm origin 还是报错的话，error: Could not remove config section 'remote.origin'. 我们需要修改gitconfig文件的内容
>4. 找到你的github的安装路径，我的是C:\Users\ASUS\AppData\Local\GitHub\PortableGit_ca477551eeb4aea0e4ae9fcd3358bd96720bb5c8\etc
>5. 找到一个名为gitconfig的文件，打开它把里面的[remote "origin"]那一行删掉就好了！




>**问题二**如果输入$ git push origin master
提示出错信息：error:failed to push som refs to .......
>1. 先输入$ git pull origin master //先把远程服务器github上面的文件拉下来
>2. 再输入$ git push origin master
>3. 如果出现报错 fatal: Couldn't find remote ref master或者fatal: 'origin' does not appear to be a git repository以及fatal: Could not read from remote repository.
>4. 则需要重新输入$ git remote add origin git@github.com:djqiang/gitdemo.git

> **问题三**如果输入$ ssh -T git@github.com出现错误提示：Permission denied (publickey).因为新生成的key不能加入ssh就会导致连接不上github。
>解决办法如下：
>1. 先输入$ssh-agent,$ssh-add ~/.ssh/id_key，这样就可以了
>2. 如果还是不行的话，输入ssh-add ~/.ssh/id_key 命令后出现报错Could not open a connection to your authentication agent.解决方法是key用Git Gui的ssh工具生成，这样生成的时候key就直接保存在ssh中了，不需要再ssh-add命令加入了，其它的user，token等配置都用命令行来做。
>3. 最好检查一下在你复制id_rsa.pub文件的内容时有没有产生多余的空格或空行，有些编辑器会帮你添加这些的。


## 三.创建项目
使用git在本地创建一个项目的过程

    $ makdir ~/hello-world    //创建一个项目hello-world
    $ cd ~/hello-world       //打开这个项目
    $ git init             //初始化 
    $ touch README
    $ git add README        //更新README文件
    $ git commit -m 'first commit'     //提交更新，并注释信息“first commit” 
    $ git remote add origin git@github.com:defnngj/hello-world.git     //连接远程github项目  
    $ git push -u origin master     //将本地项目更新到github项目上去


