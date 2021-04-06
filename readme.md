###在一台电脑配置自己的github跟公司的gitlab账号
----
- 首先找到.ssh文件(用户目录下)
- 使用git bash生成不同的ssh文件
```javascript
// 个人github  
ssh-keygen -t rsa -C "你github的邮箱" -f ~/.ssh/github_rsa （回车回车，不用管其他）
// 公司gitlab  
ssh-keygen -t rsa -C "你gitlab的邮箱" -f ~/.ssh/gitlab_rsa
```

- 打开github/gitlab添加ssh key，把刚刚生成的github_rsa/gitlab_rsa用笔记本打开，复制粘贴
- 在.ssh目录下新建config文件，内容如下
  ```javascript
	Host github.com
		HostName github.com
		User 你github的邮箱
		PreferredAuthentications publickey
		IdentityFile ~/.ssh/github_rsa
		Port 22

	Host 你gitlab的地址
		HostName 你gitlab的地址
		User 你gitlab的邮箱
		IdentityFile ~/.ssh/gitlab_rsa
		Port 你gitlab的地址的端口
```
- 测试链接
```javascript
ssh -T git@github.com
// 出现 Hi xx YOU’ve... 则成功
ssh -T git@你刚刚配的gitlab的HostName
// 出现 welcome xxx ... 则成功
```
- 删除缓存的秘钥（这一步非必须，比如您是刚刚安装git的）  
- ```javascript
 ssh-add -D
如果显示如下信息
eval $(ssh-agent)
然后重新执行第6步，如果没有报错的话，那么可以执行下面一条命令，让ssh-agent知道你有这么个key
ssh-add ~/.ssh/github_id-rsa
- ```
