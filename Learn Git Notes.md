1. 使用notepad3

2. Git————分布式版本控制系统

3. 下载Git 官网下载

4. Linus开发出了Git

5. Git Bash是命令行
  Git GUI 额 明显就是GUI了

6. 我们使用Git Bash 在这样的界面输入命令
![](https://user-gold-cdn.xitu.io/2020/2/16/1704c9dda81eb15e?w=745&h=449&f=png&s=9214)

7. “自报家门”命令
```
git config --global user.name "Name"
git config --global user.email "EmailAddress"
```
这里我使用的是gmail邮箱
`--global`这个命令表示这台机器的所有仓库用这一样的配置

8. 
  `pwd` //显示当前路径
   `cd` //转换目录（具体用法可以参见某一篇介绍cd的用法）
   `mkdir` //创建文件夹
   `dir` //显示当前路径下目录
   `ls` //与dir功能基本相同，默认带`--color`
//其实dir和ls有很多区别，本质也不一样，不过现在还不深究

9. `git init` //建立新的git仓库

10. 我们把所有需要版本控制的文件全部放在建立的git仓库目录下即可（子目录也可以）

11. `git add "filename"` //注意文件要加拓展名
    `git commit -m "explanation"` //这里的双引号加不加无所谓
	`git status` 
	`git diff`

12. `git log`
    `git log -pretty=oneline`

13. like `e56faf929daa74277c3f07a1343e788b70901ac4` is commit id

14. `HEAD` means current version  *//pay attention to capital*
    `HEAD^` means the last version   and the  rest can be done in the same manner 
    However, when we need the last 100 version ,it is too troublesome
    So we can write it as `HEAD~100`  

15. `git reset --hard HEAD^`
    `git reset --hard "commit id"`

16. `git reflog` //记录了每一次命令
这时候因为版本回退之后`git log`显示的内容就没有新的版本的内容了，要想知道commit id就必须用这个

17. `cat`      //可以显示文本

18. 暂存区
master分支
版本库
工作区

19. 用`git diff HEAD -- <file>`命令可以查看工作区和版本库里面最新版本的区别
20. `git checkout -- <file>`
*//在工作区的修改全部撤销*
*//让这个文件回到最近一次`git commit`或`git add`时的状态*
//当然我的git告诉我用`git restore <file>`也可以
//(1)一种是文件自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；
//(2)一种是文件已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。

21. `git reset`命令既可以回退版本，也可以把暂存区的修改回退到工作区
比如use `git reset HEAD <file>` to unstage
或者用`git restore --staged <file>`
//其实就相当于add的反过程

22. `rm <file>` //删除文件
    if we delete a file,Git will inform us to consider it because it still lies in the repository

23. 所以我们需要在删除文件之后`git rm <file>`或者`git add <file>`
注意这一步相当于一步`git add`,所以我们还需要`git commit`一下 
当然如果反悔的话，对应的上面的取消方法就可以了

24. 下面我们需要把本地仓库与Github相关联
当然在那之前，我们需要解决一个问题，就是我的Git默认开始路径是在用户主文件夹`C:/User/52816`里面，这里面文件太多了，处理起来就很麻烦，并且我也不想把东西放在C盘，于是我想把默认开始路径调到自定义，便参照了网上的教程

  因为我的Git是version 2.x版本，所以直接采用配置环境变量的方法
  “计算机”->“属性”->“高级系统设置”->“环境变量”->“用户变量”->“新建”

  >变量名:Home
   变量值:（就是你需要自定义的路径）

  最后一步就是把原来在用户主文件夹里面的与Git相关的文件全部拷贝到新的自定义文件夹里（例如`.ssh .gnupg. bash_history .gitconfig`等文件）

  *大功告成*

25. 继续关联
  1. 在用户主目录下找是否与`.ssh`文件夹 
  如果有，继续
  如果没有，在Git Bash输入`$ ssh-keygen -t rsa -C "youremail@example.com"`来创建SSH Key
  一路回车下来
  现在应该有了`.ssh`文件夹，并且里面有两个文件`id_rsa`和`id_rsa.pub`

  2. 在GitHub的Account settings中的SSH and GPG keys中填入信息，其中title任意填，自己明白就行了，key的话填入`id_rsa.pub`里面的信息，注意用记事本打开就行了

  3. ok啦，关联成功，

26. 下面我们在Github建一个同名的仓库，建好之后有提示，我们可以push an existing repository from the command line
 那么直接按照提示的代码输入

  ```
git remote add origin https://github.com/battlin6/repo.git
git push -u origin master
```

   	然后把本地库的内容pull进去
    `git push -u origin master`
  之后的提交就可以去掉`-u`，使用`git push origin master`即可
//当然啦Mr.Liao告诉我们用`git remote add origin git@github.com:battlin6/repo.git`来关联，这个我没试过，应该也可以
*//这个就涉及到https和@git的两种不同形式，留坑了解*

  好了好了，已经了解了，这两种是不同的协议，在GitHub的提示界面也是可以选择的
  
  ![](https://user-gold-cdn.xitu.io/2020/2/25/1707b1338db376da?w=1178&h=161&f=png&s=28239)
  ![](https://user-gold-cdn.xitu.io/2020/2/25/1707b13b19b7837e?w=1205&h=183&f=png&s=28923)
  ![](https://user-gold-cdn.xitu.io/2020/2/25/1707b11b9a4b783c?w=1192&h=155&f=png&s=17906)
  ![](https://user-gold-cdn.xitu.io/2020/2/25/1707b14c78c747de?w=1226&h=169&f=png&s=18572)

  类似于这样的形式
  不过当然还是建议用@git的模式
  >你也许还注意到，GitHub给出的地址不止一个，还可以用 https://github.com/battlin6/repo.git 这样的地址。实际上，Git支持多种协议，默认的git://使用ssh，但也可以使用https等其他协议。

  >使用https除了速度慢以外，还有个最大的麻烦是每次推送都必须输入口令，但是在某些只开放http端口的公司内部就无法使用ssh协议而只能用https。

27. 如果一不小心关联错了远程库或者想要更换，可以使用`git remote remove origin`命令
  *//毕竟基本上远程库我们都命名为了origin*
28. 刚刚说的是本地到远端，但是实际情况是我们大多都是从远端到本地，即先远程库操作，需要的时候再clone到本地