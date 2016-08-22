部署 Huginn

    克隆这个 repo

    $ git clone git@github.com:cantino/huginn.git
    $ cd huginn

    安装 Ruby and Ruby Gems (如果未安装)

    安装 rake 和 bundle (如果未安装):

    $ gem install rake bundle

    安装 Huginn 需要的依赖文件

    $ bundle install

    安装 MySQL

    启动 MySQL 服务:

    $ mysql.server start

    复制 .env.example 为 .env:

    $ cp .env.example .env

    生成 APP_SECRET_TOKEN:

    $ rake secret

    编辑 .env文件, 在 APP_SECRET_TOKEN里面填入刚才生成的 TOKEN 密匙.

    使用实例模板创建正式的 MySQL 数据库:

    $ rake db:create
    $ rake db:migrate
    $ rake db:seed

    准备就绪后. 启动本地服务:

    $ foreman start  

    访问 http://localhost:3000/ 然后使用默认的帐号和密码登录即可.
