## 利用 Cloudmailin 服务解析邮件
[Cloudmailin](https://www.cloudmailin.com/) 服务可以将邮件转化成 HTTP POST，这与 Webhook agent 结合使用的话，可以实现很多有趣的功能，具体的设置步骤如下：
* 生成一个新的 UUID（通用唯一识别码），可以使用在线服务生成，或者在终端中执行 `uuidgen` 命令生成；
* 新建一个 Webhook agent，将生成的 UUID 作为 secret，将 payload 设为 `.`，如下所示：
```
{
  "secret": "supersecretstring", # 填入前面生成的 UUID，其实，你也可以使用其他任意的字符，为安全起见，最好使用生成的 UUID
  "expected_receive_period_in_days": 1,
  "payload_path": "."
}
```
* 在 agent 的 summary 中，你将会看到类似这样的链接（URL）：`https://YOUR_DOMAIN/users/1/web_requests/15/YOUR_SECRET`；
* 在 [Cloudmailin](https://www.cloudmailin.com/) 官网注册一个新的账号；
* 注册时，在第二步 `Where shall we send your email?` 中，在 `Enter the URL of your server (HTTP Endpoint)` 中填入上面的 URL，在 `POST Format` 中选择 `JSON Format`；

直此，你已经完成了基本的设置，当你发送邮件给 Cloudmailin 提供的邮箱时，将会触发 Webhook agent ，产生事件（event）。如果你将 Webhook agent 作为触发其他 agent 的条件时，也将会触发其他 agent，从而实现自动化功能。

> 本文由 [ Huginn 中文网](http://huginn.cn) 翻译，已经获得项目作者授权，项目原文访问 [https://github.com/cantino/huginn/wiki/Parse-incoming-email-with-Cloudmailin](https://github.com/cantino/huginn/wiki/Parse-incoming-email-with-Cloudmailin)

