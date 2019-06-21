### 1.同一台电脑多账户设置
参考链接1[在一个电脑上设置两个git账户](https://blog.csdn.net/one_girl/article/details/86238676)
参考链接2[在一个电脑上设置两个git账户](#https://segmentfault.com/a/1190000016269686)
1.查询并清空全局用户名和电脑设置
```
git config --global user.name
git config --global user.email
git config   --global --unset user.name
git config --global --uset user.email
```
2.为多个账户创建分别创建sshkey，在本地添加，并把SSH key 到 github上面去
```
cd ~/.ssh
ssh-keygen -t rsa -C "your_email@example.com" 创建sshkey,不要用默认文件名，自定义一个名称，会生xxx.pub，
本地添加sshkey:
ssh-add ~/.ssh/id_rsa_one
ssh-add ~/.ssh/id_rsa_two
黏贴sshkey到github
复制里面的内容添加到github--settings--sshkey--黏贴进去就好
```
3.创建config文件,设置两个sshkey使用场景
```
touch config
内容如下：
//账户1设置
Host github_one   //Host是与HostName对应的自定义的名字，自定义，我定义的是github_one。
HostName github.com //原本的域名
User examplename1 //自定义
IdentityFile ~/.ssh/id_rsa //账户1生成的sshkey文件
//账户2设置
Host gitlab
HostName gitlab.com
User  examplename2 //自定义
IdentityFile ~/.ssh/id_rsa_2 //账户2生成的sshkey文件

```
4.远程测试
ssh -T git@gihub_one
5.clone到本地
git clone git@github.com: one的用户名/learngit.git
改成=>git clone git@域名别称：用户名/项目名
git clone git@github_one: one的用户名/learngit.git
再给这个仓库设置局部用户名和email即可
git config user.name "one_name" ;
git config user.email "one_email"
若已经down下来代码，直接重新设置name和email即可
###2.其他git设置命令
git config  --list 查询git配置信息
git config --global --replace-all user.email  "输入你的邮箱"
git config --global --replace-all user.name  "输入你的用户名"
