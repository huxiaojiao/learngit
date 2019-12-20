一.创建版本库（repository）,相当于是个目录，该目录里面的所有文件都可以被git管理起来，每个文件的修改、删除，git都能跟踪。
1.在本地选择一个合适的地方，创建一个目录：mkdir learngit
2.cd  learngit:切换到当前目录
3.git init:该命令把这个目录变成git可以管理的仓库
4.在该目录下创建一个文件并输入内容，该文件一定要放到learngit目录下（子目录也行）,如 readme.txt
5.把一个文件放到git仓库分两步：第一步git add readme.txt(告诉git,把文件添加到仓库）；
第二步git commit -m "wrote a readme file"(提交，-m后面输入的是本次提交的说明，可以输入任意内容但最好是有意义的。）
* git add <file> 可以反复添加或同时添加多个文件。
