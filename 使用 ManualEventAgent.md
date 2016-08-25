# 使用 ManualEventAgent

Manual Event Agent 是 Huginn 中最有用的工具之一， 可以用来开发和调试 agent，从而帮助开发者制作事件或传递事件给其他的 agent。通过一个任意大小或复杂程度的 JSON 格式的表单，Manual Event Agent 可以让用户精确地定义一个事件的具体内容。下面是具体的使用方法：


* 首先，新建一个 Manual Event Agent 实例。这个实例可以包含在已存在的 Scenario 中，或者是独立的。

* 将 Manual Event Agent 与待测试或调试的 agent 联系起来，方法是将其作为这个 agent 的事件源。需要记住的是，任何 agent 都可以有一个或者多个事件源。

* 在 Agents 列表或者 Scenario 图表中，点击 Manual Event Agent，然后再点击 Summary。

* 在 Option 的输入框里，输入用来描述待发送事件的 JSON 格式的内容。下面是一个简单的示例：

  	{ "message": "Hello, world!" }

* 最后，点击 Submit 按钮。这个手动创建的事件将会触发后续的事件。

> 本文由 [Huginn 中文网](http://huginn.cn) 中文网 翻译，已经获得项目作者授权，原文请访问：[Using the ManualEventAgent](https://github.com/cantino/huginn/wiki/Using-the-ManualEventAgent)

