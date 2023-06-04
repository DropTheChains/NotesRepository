在上传远程仓库的时候，出现了这个原因
![[Pasted image 20230604113649.png]]

这是由于我的远程仓库有了新的文件Redame.md添加，而本地仓库却没有与远程仓库保持一致，这时需要我们使用命令

>git pull origin master 
>先拉取一下远程仓库的分支
>再重新push
>git push  origin master

