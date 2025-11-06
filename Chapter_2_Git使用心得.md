# 1 仓库类型：gitlab 

# 2 新建项目并推送到新的gitlab远程仓库中

教程：[Git 技能：如何把本地新项目推到远程空仓库_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1iZ4y1e7J8/?spm_id_from=333.337.search-card.all.click&vd_source=b09849ba0c96cf27a23de3e43fd5066d)

# 3 从gitcode开源仓库（如jeecgboot）到gitlab官网上的私人仓库：直接用url

# 4 切换本地项目的远程仓库，并将本地项目push到新的Gitlab仓库中（即Gitlab仓库迁移）

## 4.1 场景举例

对jeecgboot开源项目进行本地改造后，推送至自己的Gitlab官网上的私人仓库。

## 4.2 几种不同方法

### 4.2.1 方法一：在git bash here中进行命令行操作

### 4.2.2 方法二：在IDEA中操作

①教程：[41-工具类_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV15W4y1479P/?spm_id_from=pageDriver&vd_source=b09849ba0c96cf27a23de3e43fd5066d)

②步骤：

     S1：idea的Git对话框中 remove remote；
     
     S2：点击 idea右上角 斜向右上箭头：添加remote，并push；
     
     S3：gitlab中出现New merge request，点进去后生成 Merge Request；
     
     S4：同意Merge；

### 4.2.3 方法三：使用TortoiseGit

①教程：[【Git教程】5-7 Git推送已有仓库到Gitee_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV15i4y1Z7jf/?spm_id_from=333.880.my_history.page.click&vd_source=b09849ba0c96cf27a23de3e43fd5066d)

②步骤：

     S1：TortoiseGit——setting——Git——remote中，删除原有remote，添加新的remote，不用修改origin名称；
     
     S2：TortoiseGit——push；
     
     S3：gitlab中出现New merge request，点进去后生成 Merge Request；
     
     S4：解决冲突，并同意Merge；

## 4.3 遇见的问题

### 4.3.1 问题描述

采取上述方法后，在将代码push之前进行pull的时候，报如下错误：You are not currently on a branch.Please specify which branch you want to merge with.See git-pull(1) for details.

**【特别注意：我的Gitlab官网上的私有仓库不是公开的，所以在push代码前最好是将Gitlab相应仓库设置为Public】**

### 4.3.2 解决措施

①参考链接：[Git常见问题解决办法 - 爱码网](https://www.likecs.com/show-389326.html)

②解决步骤：

​    S1：打开问题项目的Git Bash here；

​    S2：输入： git checkout -b temp  # 在工作区中创建并切换至temp分支；

​    S3：输入：git checkout <name>  # 切换回目标分支<name>，我的是：git checkout main；

# 5 对Git的个人理解

## 5.1 Git、小乌龟TortoiseGit的安装和中英文切换教程：

[Git、小乌龟TortoiseGit的安装和中英文切换_tortoisegit切换语言_公孙元二的博客-CSDN博客](https://blog.csdn.net/Amnesiac666/article/details/111680758)

## 5.2 个人理解

```
Git（Git管理最全面的工具）：  Git Bash here（Git的命令行界面，可以实现Git的全部操作）
                          Git GUI here（Git图形化工具，只实现部分git命令的GUI化）
                          Git Clone（Git Clone相关指令的命令栏化）
                          Git commit（Git commit相关指令的命令栏化）
                          Git syn（Git syn相关指令的命令栏化）
 TortoiseGit（基本上Git所有功能的命令栏化）
```

# 6 可参考的Git学习资料

[上传本地文件（夹）到GitHub和更新仓库文件 - 知乎](https://zhuanlan.zhihu.com/p/136355306)

[git从安装到多账户操作一套搞定（一）入门使用](https://mp.weixin.qq.com/s?__biz=MzI0MTI2MDY3NQ==&mid=2247484304&idx=1&sn=00b1ec9e2b831c1f83db6b0e501bd586&chksm=e90f027cde788b6a4707061d47b8c8ad724e4e632f233f705b63fa4901af568651a6d32b833d&scene=21#wechat_redirect)

[git从安装到多账户操作一套搞定（二）多账户使用](https://mp.weixin.qq.com/s?__biz=MzI0MTI2MDY3NQ==&mid=2247484321&idx=1&sn=e5f2da3ac99ea6c150d2d539a1385988&chksm=e90f024dde788b5bf3ebb9a1504809627a4406499bd9b5a9fe4701a5ac481bcb64e8409108b5&scene=21#wechat_redirect)

# 7 Git发版实操

## 7.1 发版方式分类

方式一：增量。示例：在gitlab上将commit从【代发版分支】（如dev）merge合并到【生产分支】（如prd），然后在【生产分支】上对commit发版，并merge commit。注：该示例中无需使用IDE。

方式二：全量。示例：将本地【代发版分支】（如dev）中的代码（最新）全量merge到本地【生产分支】（如prd），再将本地【生产分支】push到远端【生产分支】，从而全量发版。参考教程：[(54条消息) vs Code合并分支_vscode合并分支_点点辰光的博客-CSDN博客](https://blog.csdn.net/lance_heart/article/details/119574202)
