安装Git
https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/00137396287703354d8c6c01c904c7d9ff056ae23da865a000
集中式vs分布式
集中式：版本库是集中存放在中央服务器的，而干活的时候，要先从中央服务器取得最新的版本，然后开始干活，干完活了，再把自己的活推送给中央服务器。
分布式：首先，分布式版本控制系统根本没有“中央服务器”，每个人的电脑上都是一个完整的版本库。
---------------------------------------------
创建版本库
$ mkdir learngit (创建文件夹)
$ cd learngit
$ pwd （查看当前文件夹路径）
通过git init命令把这个目录变成Git可以管理的仓库：
$ git init
Initialized empty Git repository in /Users/michael/learngit/.git/
用ls -ah命令查看隐藏文件（shift+cmd+> 显示隐藏文件）
用命令git add告诉Git，把文件添加到仓库：
$ git add readme.txt
用命令git commit告诉Git，把文件提交到仓库：
$ git commit -m "wrote a readme file"
[master (root-commit) eaadf4e] wrote a readme file
 1 file changed, 2 insertions(+)
 create mode 100644 readme.txt
git commit命令执行成功后会告诉你，1 file changed：1个文件被改动（我们新添加的readme.txt文件）；2 insertions：插入了两行内容（readme.txt有两行内容）。
---------------------------------------------
时光机穿梭
git status命令可以让我们时刻掌握仓库当前的状态
$ git diff readme.txt 
工作区作出修改后，用来查看文件内容的变动（git add 前查看）
git log命令显示从最近到最远的提交日志
如果嫌输出信息太多，看得眼花缭乱的，可以试试加上--pretty=oneline参数：
$ git reset --hard HEAD^
$ git reset --hard 1094a
Git提供了一个命令git reflog用来记录你的每一次命令
如果进行如下操作：
第一次修改 -> git add -> 第二次修改 -> git commit
你看，我们前面讲了，Git管理的是修改，当你用git add命令后，在工作区的第一次修改被放入暂存区，准备提交，但是，在工作区的第二次修改并没有放入暂存区，所以，git commit只负责把暂存区的修改提交了，也就是第一次的修改被提交了，第二次的修改不会被提交。
提交后，用git diff HEAD -- readme.txt命令可以查看工作区和版本库里面最新版本的区别：
$ git commit newword.txt -m “1000”  可以直接不用 add到暂存区， 直接commit 到分支成功

git checkout -- file可以丢弃工作区的修改：
命令git checkout -- readme.txt意思就是，把readme.txt文件在工作区的修改全部撤销，这里有两种情况：
一种是readme.txt自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；
一种是readme.txt已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。
总之，就是让这个文件回到最近一次git commit或git add时的状态。
Git同样告诉我们，用命令git reset HEAD <file>可以把暂存区的修改撤销掉（unstage），重新放回工作区：
删除文件
$ rm test.txt
$ git checkout — test.txt
git checkout其实是用版本库里的版本替换工作区的版本，无论工作区是修改还是删除，都可以“一键还原”。
一是确实要从版本库中删除该文件，那就用命令git rm删掉，并且git commit：
