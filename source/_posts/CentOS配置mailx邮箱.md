## 1、获取qq邮箱授权码：

按下图的步骤获取授权码：  
![qqyx1.jpg](/img/qqyx/qqyx1.jpg) 
![qqyx2.jpg](/img/qqyx/qqyx2.jpg)

2、在Linux系统上安装mailx服务：  
在命令行直接输入 mail 指令，如果提示找不到该指令，则表示你还没有安装该服务，请使用 yum 安装该服务：

```shell
yum -y install mailx
```

3、添加qq邮箱的smtp配置：  
在系统文件 /etc/mail.rc 末尾追加下面内容（按实际情况修改成你的账号和授权码）：

```shell
set from=账号@qq.com
set smtp=smtps://smtp.qq.com:465
set smtp-auth-user=账号@qq.com
set smtp-auth-password=授权码
set smtp-auth=login
set ssl-verify=ignore
set nss-config-dir=/root/.certs
```

4、下载qq邮箱的证书：  
其实完成前面三步，已经可以发送邮件了，但是每次都会提示：

```shell
Error in certificate: Peer's certificate issuer has been marked as not trusted by the.
```

这是因为无法确认服务器证书是否真实，我们手动把证书添加到受信任列表就可以屏蔽这个提示了：

```shell
#创建存放证书的目录
mkdir -p /root/.certs

#获取邮件服务器证书
echo -n | openssl s_client -connect smtp.qq.com:465 | sed -ne '/-BEGIN CERTIFICATE-/,/-END CERTIFICATE-/p' > /root/.certs/qq.crt

#将证书添加到受信任列表
certutil -A -n "qq" -t "P,P,P" -d /root/.certs -i /root/.certs/qq.crt

#列出指定的目录下的所有证书
certutil -L -d /root/.certs
```
