

```
原来格式为表格（table），转换较复杂，未转换，需要手动复制一下
{"cells":[{"backColor":"#c5d9f2","value":"提交命令步骤"},{"backColor":"#c5d9f2","value":"描述"},{"value":"git checkout -b 001"},{"value":"在master创建一个001分支，然后代码编写","inlineStyles":{"font-family":[{"from":0,"to":23,"value":"Tahoma"}]}},{"value":"git add ."},{"value":"将代码添加到001分支"},{"value":"git commit -m \"注释\""},{"value":"提交并填写注释"},{"value":"git checkout master"},{"value":"切换到master"},{"value":"git fetch"},{"value":"拉最新代码"},{"value":"git checkout 001"},{"value":"切换到001"},{"value":"git rebase origin/master"},{"value":"合并分支"},{"value":"git add .\ngit rebase --continue"},{"value":"出现冲突时，先解决冲突，然后添加"},{"value":"git push origin 001"},{"value":"推送到远程"}],"heights":[40,40,40,40,40,40,40,40,40,40],"widths":[211,385]}
```







1.git branch 查看本地分支

-r 查看远处分支

-a 查看所有分支

-d 删除本地分支

-m oldname newname 修改本地分支名称

git branch 分支名 --创建分支



2.git checkout 分支名 切换分支

git checkout master 切换到master

-b 创建并切换分支（b-branch）



3.合并分支

git merge 分支名



4.提交

git commit -m “注释”



5.git status 显示工作目录和暂存区的状态



6.合并分支

git rebase origin/master

让分支看起来是在一条线上的，避免三角或菱形出现

merge 会把公共分支和你当前的commit 合并在一起，形成一个新的 commit 提交

rebase会把你当前分支的 commit 放到公共分支的最后面,所以叫变基。就好像你从公共分支又重新拉出来这个分支一样

 

![](https://i.loli.net/2021/08/25/8ULX4HsRnBJlGwF.png)



![](https://i.loli.net/2021/08/25/VdKi9eQTng2tBHu.png)



7.撤销修改

git restore 文件地址



8.删除文件

git clean -d -n -f

    -n 显示将要删除的文件和目录；

    -x -----删除忽略文件已经对git来说不识别的文件

    -d -----删除未被添加到git的路径中的文件

    -f -----强制运行





9.回到分支最新一次commit

git reset --hard

