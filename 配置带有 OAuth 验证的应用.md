配置带有 OAuth 验证的应用

为了使用新的 Service 集合，首先要对你想使用应用开启 OAuth 验证。

## Twitter

如果你还没有一个 Twitter 应用，先访问[https://apps.twitter.com](https://apps.twitter.com/)。

你需要给你的应用明明。可能需要类似这样的说明：`John's Huginn` 。你还需要一个说明，可以是：
`John's personal Huginn system (http://github.com/cantino/huginn)`。它所需要的网站可以是你的个人网站或者你的 Twitter 账户 URL。

回调的 URL 非常重要，你需要用 `http://<your-huginn-domain.com>/auth/twitter/callback` 来代替你的 `<your-huginn-domain.com>` 域名。

在 "API Keys" 网页你需要几下你的 "API Key" 和 "API Secret"，之后：

* 如果你的 Huginn 是自己搭建的，打开 Huginn 的 `.env` 文件，设置 `TWITTER_OAUTH_KEY` 设置成 `API Key`， `TWITTER_OAUTH_SECRET` 设置为 `API Secret`.

* 如果你使用的 Docker 容器，将 `HUGINN_TWITTER_OAUTH_KEY` 设置为 `API Key` ，`HUGINN_TWITTER_OAUTH_SECRET` 设置为 `API Secret`。[更多环境变量请查看](https://hub.docker.com/r/cantino/huginn/)

* 如果你使用的 Heroku，设置需要的环境变量到 heroku 上，`heroku config:set TWITTER_OAUTH_KEY=YOUR-KEY` 和 `heroku config:set TWITTER_OAUTH_SECRET=YOUR-SECRET`。
* 如果你使用的 OpenShift，设置需要的环境变量到，`rhc env set TWITTER_OAUTH_KEY=YOUR-KEY` 和 `rhc env set TWITTER_OAUTH_SECRET=YOUR-SECRET`.

在你重启你的 Huginn 实例之后，应该可以在 Service 页面验证你的 Twitter了。

如果遇到问题，请看下方的 [调试部分](https://github.com/cantino/huginn/wiki/Configuring-OAuth-applications#debugging-twitter)

## 37signals (Basecamp)

如果你还没有一个 37signals 应用，先访问[https://integrate.37signals.com/](https://integrate.37signals.com/) 创建一个新的。

给你的应用选择一个名字，输入你的公司名（或者你自己的名字），然后输入一个网站的网址（可以是任何的网站）。

在 "Integration" 部分，你需要开启 "Basecamp"，其他的 37signals 应用是可选择的。

在 "Redirect URI" 输入框中输入 `http://<your-huginn-domain.com>/auth/37signals/callback` 来代替你的域名 `<your-huginn-domain.com>`。

在你创建完应用后你会看到 "Client ID" 和 "Client Secret"。就像 Twitter 一样，做下面这些：

* 如果你的 Huginn 是自己搭建的，打开 Huginn 的 `.env` 文件，设置 `THIRTY_SEVEN_SIGNALS_OAUTH_KEY` 设置成 `Client ID`， `THIRTY_SEVEN_SIGNALS_OAUTH_SECRET` 设置为 `Client Secret`.

* 如果你使用的 Heroku，设置需要的环境变量，`heroku config:set THIRTY_SEVEN_SIGNALS_OAUTH_KEY=YOUR-CLIENT-ID` 和 `heroku config:set THIRTY_SEVEN_SIGNALS_OAUTH_SECRET=YOUR-CLIENT-SECRET`。
* 如果你使用的 OpenShift，设置需要的环境变量到，`rhc env set THIRTY_SEVEN_SIGNALS_OAUTH_KEY=YOUR-CLIENT-ID` 和 `rhc env set THIRTY_SEVEN_SIGNALS_OAUTH_SECRET=YOUR-CLIENT-SECRET`.

在你重启你的 Huginn 实例之后，应该可以在 Service 页面验证你的 37signals 了。

## Wunderlist

如果你还没有一个 Wunderlist 应用，先访问[https://developer.wunderlist.com/](https://developer.wunderlist.com/)，点击 ‘Register Your App’。

给你的应用选择一个名字，还需要一个应用 URL （可以是你的 huginn 实例或者其他）

在 "Authorization Callback URL" 输入框中输入 `http://<your-huginn-domain.com>/auth/wunderlist/callback` 来代替你的域名 `<your-huginn-domain.com>`。

在你创建完应用后你会看到 "Client ID" 和 "Client Secret"。就像 Twitter 一样，做下面这些：

* 如果你的 Huginn 是自己搭建的，打开 Huginn 的 `.env` 文件，设置 `WUNDERLIST_OAUTH_KEY` 设置成 `Client ID`， `WUNDERLIST_OAUTH_SECRET` 设置为 `Client Secret`.

* 如果你使用的 Heroku，设置需要的环境变量，`heroku config:set WUNDERLIST_OAUTH_KEY=YOUR-CLIENT-ID` 和 `heroku config:set WUNDERLIST_OAUTH_SECRET=YOUR-CLIENT-SECRET`。

* 如果你使用的 OpenShift，设置需要的环境变量到，`rhc env set WUNDERLIST_OAUTH_KEY=YOUR-CLIENT-ID` 和 `rhc env set WUNDERLIST_OAUTH_SECRET=YOUR-CLIENT-SECRET`.

在你重启你的 Huginn 实例之后，应该可以在 Service 页面验证你的 Wunderlist  了。

## Dropbox

如果你还没有一个 Dropbox 应用，先访问[https://developer.wunderlist.com/](https://developer.wunderlist.com/)，选择 dropbox API ，让它可以访问你的所有文件和文件夹，之后点击 ‘Create app’。

给你的应用选择一个名字，还需要一个应用 URL （可以是你的 huginn 实例或者其他）

在 "Redirect URIs" 输入框中输入 `http://<your-huginn-domain.com>/auth/dropbox/callback` 来代替你的域名 `<your-huginn-domain.com>`。

在你创建完应用后你会看到 "Client ID" 和 "Client Secret"。就像 Twitter 一样，做下面这些：

* 如果你的 Huginn 是自己搭建的，打开 Huginn 的 `.env` 文件，设置 `DROPBOX_OAUTH_KEY` 设置成 `Client ID`， `DROPBOX_OAUTH_SECRET` 设置为 `Client Secret`.

* 如果你使用的 Heroku，设置需要的环境变量，`rhc env set DROPBOX_OAUTH_KEY=YOUR-CLIENT-ID` 和 `rhc env set DROPBOX_OAUTH_SECRET=YOUR-CLIENT-SECRET`。

* 如果你使用的 OpenShift，设置需要的环境变量到，`rhc env set WUNDERLIST_OAUTH_KEY=YOUR-CLIENT-ID` 和 `rhc env set WUNDERLIST_OAUTH_SECRET=YOUR-CLIENT-SECRET`.

在你重启你的 Huginn 实例之后，应该可以在 Service 页面验证你的 Dropbox 了。

## Tumblr

为了适应 Tumblr，你必须在 huginn 的 .env 文件中声明 OAuth 的 key 和 secret。但是获得 OAuth 的 key 不是很简单，所以这里有一个过程。

首先，如果你的 Huginn 是建立于 Apache 或者 Nginx 这样基于 HTTP 验证的话，它们会限制访问，你必须使用 htpasswd 这种工具来创建一个用户名和密码来提供访问的回调 URL：`sudo htpasswd -m /path/to/.htpasswd callback`

登陆到 Tumblr 的控制中心来获得你的账户设置。点击 ”Apps“。将网页滑到网页底部，点击注册链接，[(https://www.tumblr.com/oauth/apps)](https://www.tumblr.com/oauth/apps)。点击 “+ Register application” 按钮。

在注册时输入你的应用名字（“Huginn” 是可以的）。输入一段你的应用说明；可以是任意的藐视，但是要尽量描述清楚以防止 Tumblr 单方面禁止 Huginn 使用其服务。Default Callback URL 在 Huginn 文档中没有说明，地址应该是 `https://huginn.example.com/auth/tumblr/callback`

然而，因为在访问 Huginn 之前有一个基础的 HTTP 验证，所以你需要提供用户名和密码，这样他们的 OAuth 实现可以获得回调的 URL。将 `callback:password@https://huginn.example.com/auth/tumblr/callback` 输入到 Default Callback URL 的输入框中。

完成这些之后，给你的 Huginn 上传一个图标和应用网站图标。解决 CAPTCHA。点击 Register 按钮。你会看到你的 OAuth key 和 secret。在你的 .env 文件 TUMBLR_OAUTH_KEY 和 TUMBLR_OAUTH_SECRET 填入这些，之后重启 Huginn。

登陆 Huginn，点击 Services。点击 "Authenticate with Tumblr" 按钮，并根据提示继续做。当在你需要使用的时候，返回到 Services 界面，实例化完毕 Tumblr Publish Agent 之后，你会发现 Service 部分会被填充，这时你就可以配置它了。

我建议在一个新的标签页打开 [Tumblr's API documentation](https://www.tumblr.com/docs/en/api/v2#posting) 来帮助你配置 Tumblr Publish Agent。默认的。每一个可能的配置都在 Tumblr Publish Agent 显示了。有好几个posts都是依据 Tumblr 来的，但她们不是需要同样的配置。一些选项的存在会导致 Agent 不能正确的保存，所以删除不必要的选项。如果有任何问题，把所有都设置到空或最小值。

# 调试 OAuth 应用

## [](https://github.com/cantino/huginn/wiki/Configuring-OAuth-applications#debugging-twitter)调试 Twitter

### [](https://github.com/cantino/huginn/wiki/Configuring-OAuth-applications#twitter-error-invalid-status-code-420)Twitter error: Invalid Status code 420

You may get 420 errors when you use the same Twitter credentials locally and in production, or if you're accidentally running multiple instances of the threaded worker, or perhaps if the threaded worker did not shut down properly (again causing many copies to be running).

当你在本地或者生产环境下使用同样的 Twitter 凭证时，或者偶然运行了多线程的工作，或是你的多线程工作没有正确的关闭（重复启动会造成多个运行的线程），这些都可能会得到 420 错误。

> 本文由 Huginn 中文网 翻译，已经获得项目作者授权，原文请访问：[https://github.com/cantino/huginn/wiki/Configuring-OAuth-applications](https://github.com/cantino/huginn/wiki/Configuring-OAuth-applications)。


