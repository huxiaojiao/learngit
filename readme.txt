一.创建版本库（repository）,相当于是个目录，该目录里面的所有文件都可以被git管理起来，每个文件的修改、删除，git都能跟踪。
1.在本地选择一个合适的地方，创建一个目录：mkdir learngit
2.cd  learngit:切换到当前目录
3.git init:该命令把这个目录变成git可以管理的仓库
4.在该目录下创建一个文件并输入内容，该文件一定要放到learngit目录下（子目录也行）,如 readme.txt
5.把一个文件放到git仓库分两步：第一步git add readme.txt(告诉git,把文件添加到仓库）；
第二步git commit -m "wrote a readme file"(提交，-m后面输入的是本次提交的说明，可以输入任意内容但最好是有意义的。）
* git add <file> 可以反复添加或同时添加多个文件。
* git add .->代表添加当前分支中所有的已修改文件

二.在本地进行修改
1.git status；该命令可以让我们时刻掌握仓库当前的状态。
2.git diff <file>:该命令可以查看对文件作了什么修改。
3.git log:可以查看从近到远的提交历史记录；
4.git log --pretty=oneline:可以看到更简洁的提交历史记录； 
  git log --graph：可以更直观得看到分支合并图；
5.git reset --hard HEAD^:可以把当前版本回退到上一个版本。（在git中，HEAD表示当前所在的分支，HEAD^表示当前分支的所指向的上一个版本）
6.git reset --hard <版本号前一小串数字>:可以让指针指向任意一个版本。
7.git reflog:用来记录你的每一次命令

三.概念理解
1.工作区（working directory）：即在电脑里能看到的目录
2.版本库（.git）：工作区下的一个隐藏目录，是git的版本库。该版本库里包含stage（或者叫index），master以及指向master的一个指针HEAD。
3.stage：暂存区，git add把文件添加进去实际上就是把文件修改添加到暂存区。
4.如果不把修改添加到暂存区，是无法把修改提交的。

四.撤销修改
1.有两种情况：一种是文件被修改后还没放到暂存区，撤销修改就回到和版本库一模一样的状态；
git checkout -- <file>: 意思是把文件在工作区的修改撤销。
* 注意--和文件之间一定要有空格。

2.一种是文件修改后已经被添加到暂存区，又做了修改，这时撤销修改就是回到添加到暂存区后的状态；
git reset HEAD file ：把暂存区的修改撤销掉，重新放回工作区。
* 经尝试，这时工作区的修改包括第一次和第二次的修改。

五.删除文件
1.删除文件其实也属于文件修改的一种，通常在工作区可以手动进行删除或通过命令进行删除。
版本库删除文件也是分两步：第一git rm file; 第二步 git commit -m "描述说明"

2.文件的恢复有两种情况：
如果文件从未被添加到版本库就已被删除，文件就无法恢复。
如果文件已经被添加到版本库，那么即使被删除也是可以被找回的: 
git checkout -- file(已被删除的文件）可以将文件恢复到最新版本。


六.远程仓库（github）
1.本地git仓库和github仓库之间的传输是通过ssh加密的。
在用户主目录下有.ssh目录，该目录下有id_rsa和id_rsa.pub两个文件，这两个就是ssh key的秘钥对，前者是私钥，后者是公钥。
在github中需要设置添加公钥。
为什么GitHub需要SSHKey呢？
因为GitHub需要识别出你推送的提交确实是你推送的，而不是别人冒充的，而Git支持SSH协议，所以，GitHub只要知道了你的公钥，就可以确认只有你自己才能推送。

2.先有本地库，再与远程库的关联：
通常先有了本地库时，在github上新建一个空仓库;
再根据github的提示，在本地的仓库目录下运行命令git remote add origin git@github.com:huxiaojiao/learngit.git；
再输入git push -u origin master 将本地库的所有内容推送到远程库上。（第一次使用-u参数，可以将本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时可以简化命令。）
* git 默认远程库的名字是origin。
* push之前应确保至少有一次commit才不会报错

3.先有远程库，后有本地库的关联：
首先需要知道仓库的地址：git clone git@github.com:huxiaojiao/learngit.git
* 在执行该命令时最好先切换到合适的目录下，以免造成新的仓库被放在另一个仓库的目录下。
这也是为什么当时在本地git intial 之后不能再git clone的原因，两个仓库是不能并存的。

七.关于分支
1.首先要明白分支没什么可怕的，它只是在主分支的基础上多了一个指针。分支的作用就是在多人协作的情况下会更安全和方便。
这样操作的最终目的是将分支上所做的改动合并到远程的主分支上去，这样所有人都可以看到。远程的主分支是受保护的，所以不能随便被合并，
而是需要提交merge request，然后要有权限的人进行审核进行合并。

2.接下来说一些命令：
git branch : 用来查看本地所有的分支，当前分支前会有一个*号标志
git checkout -b {分支名}： 用来新建并切换分支。记住这个命令会让新建的分支指向当前分支所在的版本，并切换到新分支。
git branch {分支名}：用来新建分支。跟上面的区别点是只新建但不切换分支。
git checkout {分支名}：用来切换分支。需要记住一点如果在新增分支时，当时的版本存在未提交的文件，在新分支做了改动后，
需要将所有的改动都提交后才能切换分支，否则会提示错误。
git merge {分支名}：该命令会将分支的改动合并到当前分支，这里默认使用fast forward 模式。
git branch -d {分支名}：用来删除该分支，删除成功的前提是已经merge成功了
git branch -D {分支名}：如果该分支未被合并，该命令可以用来强行删除分支

3.解决冲突：
如果两个分支分别对同一个文件进行了修改，并且都做了提交，这时想将其中一个分支合并到主分支就会出现冲突。解决冲突就是找到产生冲突的文件，
将里面的文件手动修改为我们所希望的样子，这时可能需要做一些取舍，需要结合其他人对这个文件的修改做一个衡量。修改后，再做一次添加和提交，这时就合并成功了。

4.合并分支有两种模式：fast forward 和 no-ff模式。前者在合并时就是将当前分支的指针指向要合并的分支所在的节点，这样的话不会新产生节点。后者则是会产生新的节点。
git merge --no-ff -m '{描述语言}' {某分支}：该命令表示禁用快速前进模式。
合并分支时，加上--no-ff参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，而fast forward合并就看不出来曾经做过合并。