## 与外部软件结合起来使用 Webhook Agent

一般地，通过使用 Webhook Agent，你可以将任意数据导入进 Huginn 中进行加工处理。当数据通过POST的方式发送给 Webhook Agent 时，将会产生一个或多个事件或者触发其他的 Agents。你可以把 Webhook  Agent 当作成普通的 REST API 端点，通过触发这样的端点来实现相应的功能。在实践中，我们通过 POST 一个 JSON 文件给 Webhook Agent，利用键-值就可以在 Huginn 中完成其他操作。

### Webhook Agent URLs

Webhook Agent 产生的链接（URLs）的样式是这样的：`https://huginn.example.com/users/1/web_requests/948/neverGonnaGiveYouUp`，下面对该URL做以下几点解释：
* URL中的`/users/1`部分代表的是 Huginn 用户，`/users/1`指的是 Huginn 网站的管理员（admin），`/users/2`指的是创建的第二个用户，其他的以此类推。
* The /web_requests/ part of the Huginn URI can be interpreted to mean "REST API rail for Webhook Agents.
* `/948/`代表的是 Huginn agent 的编号（这里的agent编号为948），对于不同的 Webhook Agent，该数字也是不同的。
* 在 Webhook Agent 的配置中，`secret`相当于 API key，用来认证来着外部的连接。针对不同的 Webhook Agent，最好使用不同的 `secret`，以防被其他人识破，这相对于一个密码。
* If you have a web server in front of Huginn acting as a reverse proxy and implementing HTTP auth, and your Webhook Agent needs to be accessible from the public Net, you'll have to set up an HTTP auth account which can be used to log in from outside (see also ticket #815). Then your URLs will look like this: `https://webhookuser:webhookpassword@huginn.example.com/users/1/web_requests/948/neverGonnaLetYouDown`
* You can also write code which runs on the same host as Huginn and not have to worry about HTTP auth: `http://localhost:3000/users/1/web_requests/948/neverGonnaRunAroundAndDesertYou`

### 向 Webhook Agent 发送请求

目前，Webhook Agent支持下面两种HTTP方式：
* POST（默认）
* GET

**通过 POST 的方式连接 Webhook Agent 的必须是 JSON 格式的文件，所有向 Webhook Agent 的 HTTP 请求必须带有`Content-Type: application/json`的 HTTP header，否则可能会产生一些奇怪的错误。**

### 使用案例：

假如你需要在 python 中与 Webhook Agent 进行交互，使用 [Requests](http://docs.python-requests.org/en/latest/) 模块进行请求，则可以参照下面的代码：

```
search_results = ["https://www.example.com/", "http://site.example.com"]
custom_headers = { "Content-Type": "application/json" } # HTTP header
results = { "results": search_results }
request = requests.post(webhook, data=json.dumps(results), headers=custom_headers) # 通过requests模块实现POST请求
```

> 本文由 [Huginn 中文网](http://huginn.cn) 翻译，已经获得项目作者授权，项目原文访问 [Using a Webhook Agent with external software](https://github.com/cantino/huginn/wiki/Using-a-Webhook-Agent-with-external-software)

