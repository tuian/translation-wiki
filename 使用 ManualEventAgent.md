使用 ManualEventAgent

在 Huginn 中，Manual Event Agent 是一个用来开发和调试 agent 网络的工具。它可以用来让开发者做一些事件，还可以传递事件给其他的 agent。Manual Event Agent 允许用户通过一个 JSON 文件的表单，去指定一个事件明确的内容，比如这个事件的任意大小或者复杂度。下面是如何使用：

* 实例化一个 Manual Event Agent 实例。这个可以是一个存在的 Scenario 或者是任意的。

* 将 Manual Event Agent 作为一个其他事件的来源。这样就把 Manual Event Agent 和其他 agent 联系起来，用来测试或者调试。要记住任何agent都可以有一个或者多个事件源。

* 在 Agents 列表里或者 Scenario 图表里，点击 Manual Event Agent，之后点击 Summary。

		{ "message": "Hello, world!" }

* 在 Option 的输入框里，输入 JSON 文档，用来描述事件。下面是一个简单的示例：
		
		{ "message": "Hello, world!" }

* 点击 Submit 按钮。这个事件将会被创建，之后会在事件链中向后面传递。

本文由 Huginn 中文网 翻译，已经获得项目作者授权，原文请访问：[https://github.com/cantino/huginn/wiki/Using-the-ManualEventAgent](https://github.com/cantino/huginn/wiki/Using-the-ManualEventAgent)。

