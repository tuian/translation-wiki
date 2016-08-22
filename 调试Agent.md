# 调试 Agent

假如我们写了一个彗星撞地球会触发的 Agent .
但是上一次的彗星撞地球事件,
Agent 遇到了错误,不能触 发event.
如果你不想在触发错误,最好要去调试.


如果你认为你的 Agent 有 bug , log() 或 errors.add() 是有用的.
然后使用 web 页面运行你的 Agent(Actions -> Run) , 检 查Log 信息 (Actions -> Show -> Logs).

你也能用一个通用的 Agent 去手动触发事件运行.

最后,所有日志消息和错误信息可以在 
huginn/log/development.log 
查看, 
但是这个文件很难筛选出单独 Agent 的 log 信息.

需要做的:

详细解释 between log() 与 errors.add() 的差异
