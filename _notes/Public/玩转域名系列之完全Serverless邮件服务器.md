---
notetype: feed
title: 玩转域名系列之完全Serverless邮件服务器
date: 2022-04-05 

---
#Domain #Mailserver

   买了域名又不知道除了写博客还能干什么？ 今天写一下如何利用免费的服务*并且使用Gmail*实现用自己的域名自定义的邮箱来收发邮件。而且不需要懂太多的技术，点点点即可。


__为什么不自建邮件服务器？__
不想写废话，网上已经说的很清楚了。
```
https://poolp.org/posts/2019-08-30/you-should-not-run-your-mail-server-because-mail-is-hard/
```


**前提条件**
1. 一个自己的域名。 
2. 一个cloudflare账号（免费即可）。
3. 一个Gmail账号。

**实验环境**
1. 域名： example.com
2. 自定义邮件：admin@example.com
3. Gmail：example@gmail.com


Step1  实现收取自定义邮箱邮件的设定：
按照以下步骤来操作，有各种语言版本的翻译，就不重复造轮子了。
~~~
https://blog.cloudflare.com/introducing-email-routing/
~~~

完成这一步后，向example.com发邮件就会被转发到example@gmail.com。但是此时回复的话发件人依旧是example@gmail.com。

Step2  实现用自定义邮箱发件的设定：

1. 在DNS记录里添加如下 SPF记录

`v=spf1 include:spf.hanami.run include:_spf.google.com ~all`

2.获取谷歌程序认证密码
`https://myaccount.google.com/apppasswords`
*这一步需要账户已经启用了MFA二段验证，如果没有启用，需要先开启MFA。
`https://support.google.com/accounts/answer/185839?hl=zh-Hans&co=GENIE.Platform%3DDesktop`


3.打开Gmail
定位到 `设置 → 账号和导入 → 用这个地址发送邮件 → 添加其他电子邮件地址`

