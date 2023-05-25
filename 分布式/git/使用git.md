## git

##### 版本回退

* git log 历史记录 显示每次提交时的日志

  * git log --pretty=oneline 只显示commit id 和日志

* git reset 退回到上一个版本

  * git reset --hard HEAD^

  * git log 看不到之后的版本了

* 要想恢复的话

  1. 命令行窗口没有关掉

  * 找到要恢复的commit id
  * git reset --hard <commit id>
    * commit id 不用全部写完, 写几位就好了

  2. 命令行已经关掉

  * git reflog 显示记录的每次命令




##### 删除文件

* 再文件管理器中直接删除, 或者 rm test.txt

  * 使用 git status 可以查看被删除的文件

* 从版本库中删除 git rm text.txt, 并且 git commit

* 恢复 git checkout -- text.txt   git checkout 其实是用版本库的文件替换工作区中的文件

  

##### 远程厂库

每个人都将在远程仓库中克隆一份到自己的电脑上, 并且各自把各自的提交推送到远程厂库, 也从远程仓库中拉去别人的提交

* 先再github上创建一个厂库

* 要关联一个远程库，使

  * ```
    $ git remote add origin(远程关联名) git@github.com:lihaoliaho/仓库名.git
    ```

    * `origin`是默认习惯命名；

      

* ```
  git push -u origin main
  ```

  * 由于远程库是空的，我们第一次推送`master`分支时，加上了`-u`参数，Git不但会把本地的`master`分支内容推送的远程新的`master`分支，还会把本地的`master`分支和远程的`master`分支关联起来，在以后的推送或者拉取时就可以简化命令

* 从现在起，只要本地作了提交，就可以通过命令：

  ```
  $ git push origin master
  ```



##### 删除远程库

* 如果添加的时候地址写错了，或者就是想删除远程库，可以用`git remote rm <name>`命令。使用前，建议先用`git remote -v`查看远程库信息：

* 然后，根据名字删除，比如删除`origin`：

  ```
  $ git remote rm origin
  ```

  * 此处的“删除”其实是解除了本地和远程的绑定关系，并不是物理上删除了远程库。远程库本身并没有任何改动。要真正删除远程库，需要登录到GitHub，在后台页面找到删除按钮再删除



##### 分支管理

* 介绍: 
  * 假设你准备开发一个新功能，但是需要两周才能完成，第一周你写了50%的代码，如果立刻提交，由于代码还没写完，不完整的代码库会导致别人不能干活了。如果等代码全部写完再一次提交，又存在丢失每天进度的巨大风险. 
  * 现在有了分支，就不用怕了。你创建了一个属于你自己的分支，别人看不到，还继续在原来的分支上正常工作，而你在自己的分支上干活，想提交就提交，直到开发完毕后，再一次性合并到原来的分支上，这样，既安全，又不影响别人工作。

* 使用

  * 创建dev分支 创建并切换到dev
    * git checkout -b dev

      ---

  * 创建dev
  
    * git branch dev(分支名称)
  
  * 切换到dev上
  
    * git checkout dev
  
    ---
  
  * 查看分支
  
    * git branch
    * 在dev 分支上提交
  
  * dev上工作完成, 切回master分支
  
    * git checkout master
    
  * 将dev分支中的工作合并到master上
  
    * git merge dev
      * `git merge`命令用于合并指定分支到当前分支
  
  * 删除dev指针
  
    * ```
      git branch -d dev
      ```
  
  * git branch 再次查看分支



---

* git switch

  * 实际上，切换分支这个动作，用`switch`更科学。因此，最新版本的Git提供了新的`git switch`命令来切换分支：

    创建并切换到新的`dev`分支，可以使用：

    ```
    $ git switch -c dev
    ```

    直接切换到已有的`master`分支，可以使用：

    ```
    $ git switch master
    ```

* 小结

  Git鼓励大量使用分支：

  查看分支：`git branch`

  创建分支：`git branch <name>`

  切换分支：`git checkout <name>`或者`git switch <name>`

  创建+切换分支：`git checkout -b <name>`或者`git switch -c <name>`

  合并某分支到当前分支：`git merge <name>`

  删除分支：`git branch -d <name>`



##### 解决冲突

* 当Git无法自动合并分支时，就必须首先解决冲突。解决冲突后，再提交，合并完成。

  解决冲突就是把Git合并失败的文件手动编辑为我们希望的内容，再提交。

  查看文件:Git用`<<<<<<<`，`=======`，`>>>>>>>`标记出不同分支的内容，我们修改如下后保存：

  用`git log --graph`命令可以看到分支合并图。



##### 分支管理策略

所以，团队合作的分支看起来就像这样：

![git-br-policy](https://www.liaoxuefeng.com/files/attachments/919023260793600/0)



Git分支十分强大，在团队开发中应该充分应用。

合并分支时，加上`--no-ff`参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，而`fast forward`合并就看不出来曾经做过合并。



##### bug分支

工作只进行到一半，还没法提交，预计完成还需1天时间。但是，必须在两个小时内修复该bug，怎么办？

* git stash 将当前工作现场“储藏”起来，等以后恢复现场后继续工作：

* 小结
  * 修复bug时，我们会通过创建新的bug分支进行修复，然后合并，最后删除；当手头工作没有完成时，先把工作现场`git stash`一下，然后去修复bug，修复后，再`git stash pop`，回到工作现场；在master分支上修复的bug，想要合并到当前dev分支，可以用`git cherry-pick <commit>`命令，把bug提交的修改“复制”到当前分支，避免重复劳动。



##### 多人协作

* 多人在同一个分支上协作时，很容易出现冲突。即使没有冲突，后push的童鞋不得不先pull，在本地合并，然后才能push成功。

