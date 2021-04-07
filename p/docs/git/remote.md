## git远程仓库的一些记录


```sh
#添加github
git remote add origin https://github.com/xxx(仓库地址)

#添加多个库，一并推送
git remote set-url --add origin https://git.gitee.com/xxxx(仓库地址)

#提交
git push origin master(分支名)
```



### 遇到拉取远程报错
> fatal: refusing to merge unrelated histories
```sh
git pull origin master --allow-unrelated-histories
```