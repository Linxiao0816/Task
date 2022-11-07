# Git基础知识体系
## 1.什么是Git
Git是目前世界上最先进的分布式版本控制系统。  
什么是版本控制系统？  
***自动帮我记录每次文件的改动，还可以让同事协作编辑***，这样就不用自己管理一堆类似的文件了，也不需要把文件传来传去。如果想查看某次改动，只需要在软件里瞄一眼就可以。
## 2.Git基本指令及含义
- cd 进入一个目录 
- mkdir 创建一个目录
- git init 把这个目录变成可管理的仓库
- git add 将一个文件添加到暂存区
- git commit 将暂存区文件上传到仓库
- git branch -m 原名 新名字 改分支名字
- git status 查看当前项目中源代码的情况
- git branch -a 查看本地和远程分支
- git remote 管理远程仓库(查看分支)
- git remote -v 查看分支及对应网址
- git push remote branch 将本地分支推送到远程仓库（第一次推送的时候加上 -u参数，这样可以关联起来
- git pull remote branch 获取远程仓库分支
- ssh -T (-v)git@github.com 查看ssh是否连接成功(查看详细情况)
- vim(config) 进入文档编辑器(编辑一个配置文件)

## 3.初学git时遇到的一些问题及总结
- 第一次尝试将本地文件推送到远程仓库时遇到过不少报错。
1. 比如我在下载git之初时设置了分支名，我根据自己喜好随便取了一个"cool"（当时我还不知道这个名字是干什么用的）后来在报错后查阅资料发现，当远程仓库分支与本地分支名字不一致时，会出现报错。
>git OpenSSL SSL_read: Connection was reset, errno 10054。  
2. 报错如上字面意思链接重置（大概是说我传输不安全的意思吧），当时也是很懵，查阅后，解决方法就是使用*ssh密匙*进行传输。将 .git中的config文件中的url后面的地址改为我自己创建的SSH密匙地址。
> [解决ssh密匙配置问题时查阅的资料](https://blog.csdn.net/weixin_43325510/article/details/121129094?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522166730774416782395358193%2522%252C%2522scm%2522%253A%252220140713.130102334.pc%255Fall.%2522%257D&request_id=166730774416782395358193&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~first_rank_ecpm_v1~rank_v31_ecpm-1-121129094-null-null.142^v62^js_top,201^v3^control_2,213^v1^t3_esquery_v3&utm_term=git%20%E8%A7%A3%E9%99%A4ssl%E9%AA%8C%E8%AF%81&spm=1018.2226.3001.4187)
3. git pull的使用很重要，这是我在教程上面没有看到的，以至于屏幕上出现各种报错时我不明所以，事实上，至少在我的电脑上，在使用git push推送之前，需要先用git pull进行抓取。
> ssh: connect to host github.com port 22: Connection timed out

4. 今天遇到的新问题，ssh的22号端口被封锁了(没用两次就被锁了)，我查完资料本来以为是个很简单的问题，自己重新配置端口就行了。[参考文献](https://blog.csdn.net/qq_31020665/article/details/114113108?ops_request_misc=&request_id=&biz_id=102&utm_term=ssh:%20connect%20to%20host%20github.co&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduweb~default-0-114113108.142^v63^js_top,201^v3^control_2,213^v1^t3_esquery_v3&spm=1018.2226.3001.4187)(*话说为什么是443端口呢，我查看了两个不同博主的文献，都是用443这个数字*)  
***结果！！！！！***  
***没想到这个问题折磨了我整整三个小时！！！！***  
> Connection reset by 20.205.243.160 port 443

按照教程重新配置端口以后，问题并没有得到解决，我继续搜索，在许多种相同的解决方案中，我找出第二种说法：在防火墙处新建一个入站规则，端口设为ssh使用的端口。  
***然而问题还是没有解决！！！！！！***  
最终，尝试了重启电脑，重新登入管理员账户，等等一系列胡乱操作后，我抱着最后一线希望在CSDN中胡乱寻找，发现了一个不那么靠谱的说法——
> “可能根本不是你电脑的问题，就是你连接的wifi不支持。”[参考文献](https://blog.csdn.net/zj57356498318/article/details/100513450?ops_request_misc=&request_id=&biz_id=102&utm_term=Connection%20reset%20by%2020.205.243&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduweb~default-0-100513450.142^v63^js_top,201^v3^control_2,213^v1^t3_esquery_v3&spm=1018.2226.3001.4187)

~~没错，你可能不信。  
这就是最终答案~~   
peace.