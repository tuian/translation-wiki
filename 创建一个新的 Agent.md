# 创建一个新的 agent

*请注意：Huginn 的 API 正在进行更改，因此一些无用的 Agent 将被放弃。我们非常希望您能将您的使用方法以及 API 应该更改什么告诉我们。查看 [#60](https://github.com/cantino/huginn/issues/60) 和 [#293](https://github.com/cantino/huginn/issues/293)。*

Huginn 的 Agent 能创建和接受事件。并且能在特定的时间运行一定规范的代码。创建一个 Agent 不是很难，你可以很轻松的从一个已存在的 Agent 创建一个子 Agent。

Agent 保存在 `app/models/agents`，RSpec 保存在 `spec/models/agents`。

# 描述

使用 `description` class method 设置你的 Agent 描述。例如：

    description <<-MD
      The WeatherAgent creates an event for the following day's weather at `zipcode`.

      You must setup an API key for Wunderground in order to use this Agent.
    MD

# 选项

Agent 是用户的 JSON 配置， 通过 [[Liquid|Formatting Events using Liquid]] 进行一些安全的 `options` 替换。你应该定义一个 `default_options` 方法， 该方法能返回一个默认的配置作为例子。你应该定义一个 `validate_options` 方法，该方法会验证 `options` 的内容。如果字段是必填的，并且你不想用默认值替换，请看下面的实例：

    def default_options
      { 'zipcode' => '94103' }
    end

    def validate_options
      errors.add(:base， 'zipcode is required') unless options['zipcode'].present?
    end

# 时间表

Agent 会在一定的时间或一定的时间间隔运行.当一个时间被触发，你的 Agent 内的 `check` 方法将会运行。如果你的 Agent 是可用的，将会使用 `default_schedule` 方法，否则会调用 `cannot_be_scheduled!` 方法。可用的时间如下：`every_1m`， `every_2m`， `every_5m`， `every_10m`， `every_30m`， `every_1h`， `every_2h`， `every_5h`， `every_12h`， `every_1d`， `every_2d`， `every_7d`， `midnight`， `1am`， `2am`， `3am`， `4am`， `5am`， `6am`， `7am`， `8am`， `9am`， `10am`， `11am`， `noon`， `1pm`， `2pm`， `3pm`， `4pm`， `5pm`， `6pm`， `7pm`， `8pm`， `9pm`， `10pm`， `11pm`。

    default_schedule "8pm"

    def check
      wunderground.forecast_for(interpolated['zipcode'])['forecast']['simpleforecast']['forecastday'].each do |day|
        if is_tomorrow?(day)
          create_event :payload => day.merge('zipcode' => interpolated['zipcode'])
        end
      end
    end

如果你的Agent创建了事件，(实例 [WeatherAgent](https://github.com/cantino/huginn/blob/master/app/models/agents/weather_agent.rb) )你应该使用 `event_description` 方法作为你的时间的包含内容。

    event_description <<-MD
      Events look like this:

          {
            'zipcode' => 12345，
            ...
            'maxhumidity' => 93，
            'minhumidity' => 63
          }
    MD

# 接受事件

如果你的Agent能接受事件，定义 `receive` 方法，该方法接受事件的 array，否则注释 `receive` 方法，将调用 `cannot_receive_events!` 方法。

# 创建事件

在代码中你的 Agent 可以通过 `create_event :payload => { ... }` 创建事件。否则注释它，将调用 `cannot_create_events!` 方法。

# 内存

Agent 拥有内存池，内存池可以在时间间隔或接受事件之间保持状态。如果你有空的内存，Agent将自动保存和读取。

# 日志

你的 Agent 应该创建日志，当有趣的事情或错误发生的时候。调用 `log` 或 `error` 信息，可选的，`:outbound_event` 或 `:inbound_event` 可以监测日志信息。

# 正在工作吗?

如果你的 Agent 的实例工作的很好，那么将此状态告诉用户是很好的。你应该定义 `working?` 方法，当一切正常的时候该方法返回 true。这里有一个功能是创建事件并有一个 `expected_update_period_in_days` 选项的 Agent 的 `working?` 方法示例。

    def working?
      event_created_within?(interpolated['expected_update_period_in_days']) && !recent_error_logs?
    end

这里有一个功能是接受事件并有一个 `expected_receive_period_in_days` 选项的 Agent 的 `working?` 方法示例。

    def working?
      last_receive_at && last_receive_at > interpolated['expected_receive_period_in_days'].to_i.days.ago && !recent_error_logs?
    end

当然，你也可以写一些特殊的代码在 `working?` 方法中。

# UI

Agent 的 UI 保存在 `app/views/agents/agent_views/<agent name>/_show.html.erb`。如果你需要一些服务器端的功能，你可以 POST 数据到 `handle_details_post_agent_path`，在你的 Agent 的 `handle_details_post` 方法中使用。查看示例在 [ManualEventAgent](https://github.com/cantino/huginn/blob/master/app/models/agents/manual_event_agent.rb) 和 [details view](https://github.com/cantino/huginn/blob/master/app/views/agents/agent_views/manual_event_agent/_show.html.erb)。

# 接收web请求

你的 Agent 可以接收 web 请求，通过 `receive_web_request`。你的 Agent URL 类似 `http://yourserver.com/users/:user_id/web_requests/:agent_id/:secret`， `:user_id` 是用户的 ID， `:agent_id` 是 Agent 的 ID，`secret` 是用户的特殊 token，在 `receive_web_request` 中被验证。推荐每次 `receive_web_request` 调用都验证 token。例如，你的 Agent 的一个选项叫做 `secret`，你可以通过比较这个值过滤掉无效的请求，
你的Agent的 `receive_web_request` 方法应该返回一个数组 (status， MiME type) 作为响应，示例如下：

    [{ status: "success" }， 200]

或

    ["not found"， 404， 'text/plain']

这里有一个 `receive_web_request` 例子如下：

```ruby
def receive_web_request(params， method， format)
  secret = params.delete('secret')
  return ["Please use POST requests only"， 401] unless method == "post"
  return ["Not Authorized"， 401] unless secret == interpolated['secret']

  # do something with params here

  ['Done!'， 200， 'text/plain']
end
```

如果你需要从请求中获得更多的参数，也可以定义 `receive_web_request` 方法如下：

```
def receive_web_request(request)
end
```

Please see the [WebRequestsController](https://github.com/cantino/huginn/blob/master/app/controllers/web_requests_controller.rb) for more documentation， as well as the implementations of `receive_web_request` in [WebhookAgent](https://github.com/cantino/huginn/blob/master/app/models/agents/webhook_agent.rb) and [DataOutputAgent](https://github.com/cantino/huginn/blob/master/app/models/agents/data_output_agent.rb).

> 本文由 [ Huginn 中文网](http://huginn.cn) 翻译，已经获得项目作者授权，项目原文访问 [https://github.com/cantino/huginn/wiki/Creating-a-new-agent](https://github.com/cantino/huginn/wiki/Creating-a-new-agent)

