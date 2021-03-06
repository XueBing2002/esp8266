# git 学习笔记10.12

office

## git 常用命令

>>#### 将所有文件添加到暂存区
	git add 
>>#### 提交到本地仓库
	git commit -m "版本描述"
>>>>###### 修正最近一次错误的版本描述
	git commit --amend -m "正确的版本描述"	
>>#### push到远程main分支
	git push origin main

>>#### 删除文件
	git rm FileName
>>#### 文件重命名
	git mv oldName  newName

## git 分支操作
>>#### 查看分支
	git branch
>>#### 创建分支
        git branch branch01
>>#### 切换分支
        git checkout -
	git checkout branch01
>>#### 合并分支branch01(合并到当前分区)
	git merge branch01
>>#### 删除分支branch01
	git branch -d branch01 
        git branch -D branch01 #强制删除,慎用
 

>>#### 检出分支branch01并切换
	git checkout -b branch01
>>>>###### 等同于下面两条命令：
	git branch branch01
	git checkout branch01

## git 帮助
	git help
	git branch -help   (获取git branch命令的更多参数)  
	git help config  (web)
	git config --help (windows下未验证)
	man git-config   (windows下未验证)


### 对某个文件取消跟踪

	git rm --cached readme1.txt    删除readme1.txt的跟踪，并保留在本地。

### 忽略文件
    工作目录建立 .gitignore，将需要忽略文件名输入其中，支持通配符 *





## git 命令行回退到某个指定的版本

1、在开发过程中遇到合并别人的代码或者合并主分支的代码导致自己的分支代码冲突或有别的问题，这时我们需要回退某个git提交历史的代码 用一下命令

	git reset --hard commitID

commitID是git提交的历史版本号，上git上面找到复制下来就行


2、执行上面操作之后我们本地的代码就会回到你需要回到的某个版本的代码

但是只是我们本地的代码回退了 如果需要push到远端需要执行以下操作

	git push -f -u origin master

(需要push到远端的分支)
强制提交到master分支,远端的分支将会被替换，

注意：这里我们要注意，当我们执行了第二步操作之后，远端的代码就已经被强制替换掉 在 “ 139dcfaa558e3276b30b6b2e5cbbb9c00bbdca96  “之后提交的分支git提交历史上就找不到了 所以我们强制推到远端一定要记得备份代码







## git 清空所有commit记录方法

说明：例如将代码提交到git仓库，将一些敏感信息提交，所以需要删除提交记录以彻底清除提交信息，以得到一个干净的仓库且代码不变

	git checkout --orphan latest_branch		#1. Checkout
	git add -A								#2. Add all the files
	git commit -am "commit message" 		#3. Commit the changes
	git branch -D master 					#4. Delete the branch
	git branch -m master 					#5. Rename the current branch to master
	git push -f origin master				6. Finally, force update your repository





## git 常见错误
 > ### 网络错误

	git push origin main
ssh: connect to host github.com port 22: Connection timed out
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
and the repository exists.



 > git push错误
fatal: refusing to merge unrelated histories
（拒绝合并不相关的历史）
解决方法：

	git push origin main --allow-unrelated-history


<details>
<summary>
展开查看
</summary>
<pre><code>
dfasdfasfdas
fddsfasfdasfd
asdfasfdasfdas
</code></pre>
</details>






