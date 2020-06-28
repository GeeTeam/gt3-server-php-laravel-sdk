# gt3-server-php-laravel-sdk

## 示例部署环境
条目|说明
----|----
操作系统|ubuntu 16.04.6 lts
composer版本|1.10.7
php版本|7.2.24
laravel版本|5.5.8

## 部署流程

### 下载sdk demo
```
git clone https://github.com/GeeTeam/gt3-server-php-laravel-sdk.git
```

### 配置密钥，修改请求参数
> 配置密钥

从[极验管理后台](https://auth.geetest.com/login/)获取公钥（id）和私钥（key）, 并在代码中配置。配置文件的相对路径如下：
```
app/Http/Controllers/geetest_config.php
```

> 修改请求参数（可选）

名称|说明
----|------
user_id|客户端用户的唯一标识，作用于提供进阶数据分析服务，可在register和validate接口传入，不传入也不影响验证服务的使用；若担心用户信息风险，可作预处理(如哈希处理)再提供到极验
client_type|客户端类型，web：电脑上的浏览器；h5：手机上的浏览器，包括移动应用内完全内置的web_view；native：通过原生sdk植入app应用的方式；unknown：未知
ip_address|客户端请求sdk服务器的ip地址

### 关键文件说明
名称|说明|相对路径
----|----|----
GeetestController.php|接口请求控制器，主要处理验证初始化和二次验证接口请求|app/Http/Controllers/
geetest_config.php|配置id和key|app/Http/Controllers/
GeetestLib.php|核心sdk，处理各种业务|app/Http/Controllers/Sdk/
GeetestLibResult.php|核心sdk返回数据的包装对象|app/Http/Controllers/Sdk/
index.html|demo示例首页|public/
web.php|路由设置，首页、验证初始化和二次验证接口|routes/
VerifyCsrfToken.php|中间件，跳过二次验证接口csrf校验(可自行设计添加)|app/Http/Middleware/
laravel.log|记录关键流程日志|storage/logs/
.env|框架配置文件（自行设计更改）|
composer.json|依赖管理配置文件|

### 运行demo
```
cd gt3-server-php-laravel-sdk
sudo cp .env.example .env
sudo composer install
sudo php artisan serve --host=0.0.0.0 --port=8889
```
- 在浏览器中访问`http://localhost:8889`即可看到demo界面。
- 查看日志`tail -f storage/logs/laravel.log`

## 发布日志

### tag：20200701
- 统一各语言sdk标准
- 版本：php-laravel:3.1.0

