我在gitpush项目的时候，将一些配置文件也进行了上传，那么怎么将这些配置文件在git中删除呢？
使用命令：
```shell
这里以.idea文件作为示例

git rm -r --cached .\.idea\

执行命令后 就将.idea删除了，之后我们再使用
修改.gitignore 忽略.idea

git status
查看git状态

会发现.idea文件未被追踪了 然后我们git commit

发现.idea文件都被delete掉了
再看看我们的GitHub仓库，dev分支已经没有.idea文件了
完美解决

```

![[Pasted image 20230603215844.png]]

![[Pasted image 20230603220133.png]]

![[Pasted image 20230603220446.png]]
