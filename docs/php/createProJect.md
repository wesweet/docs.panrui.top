<!--
 * @Description: php项目目录结构
 * @Author: panrui
 * @Date: 2021-11-18 15:56:21
 * @LastEditTime: 2021-11-23 11:02:40
 * @LastEditors: panrui
 * 不忘初心,不负梦想
-->

## 项目文档

### 1.1 准备工作

> 开发环境

```php
php >= 7.1.3//测试、正式环境要求固定为7.1.8
```

> 工具

- composer
  - 安装 <a href="https://pkg.phpcomposer.com/#how-to-install-composer" target="_blank">【详细安装文档】</a>
  ```bash
  php -r "copy('https://install.phpcomposer.com/installer', 'composer-setup.php');"
  php composer-setup.php
  #全局安装(Mac 或 Linux)
  sudo mv composer.phar /usr/local/bin/composer
  #全局安装(Windows)
  ##1.找到并进入 PHP 的安装目录（和你在命令行中执行的 php 指令应该是同一套 PHP）。
  ##2.将 composer.phar 复制到 PHP 的安装目录下面，也就是和 php.exe 在同一级目录。
  ##4.在 PHP 安装目录下新建一个 composer.bat 文件，并将下列代码保存到此文件中。
  @php "%~dp0composer.phar" %*
  ```
  - 使用 <a href="https://pkg.phpcomposer.com/" target="_blank">【详细使用文档】</a>
  ```bash
  #全局镜像设置
  composer config -g repo.packagist composer https://mirrors.aliyun.com/composer/
  #当前项目镜像设置
  composer config repo.packagist composer https://mirrors.aliyun.com/composer/
  ```

### 1.2 创建空白项目

```bash
composer create-project --prefer-dist laravel/laravel api-test.mujoy.com/ "5.6.*"
```

> ⚠️ 如需要指定 php 和 compser 文件执行可参照以下示例

```bash
/Applications/MAMP/bin/php/php7.1.32/bin/php /usr/local/bin/composer create-project --prefer-dist laravel/laravel api-test.mujoy.com "5.6.*"
```

### 1.2 项目目录规范

> _常见目录及文件结构见下:_ _(⚠️ 标红为必要配置;标蓝为主要配置;标灰为次要配置)_

📁 app/

> 📁 Console/

> 📁 Exceptions/

> 📁 Http/
>
> > 📁 Controllers/

> > 📁 Middleware/

> > Kernel.php<font color=blue>【如有需要配置路由访问中间间件，详情见 1.2.1】</font>

> 📁 Providers/

> 📁 Jobs/<font color=blue>【如有需要根据 artisan 命令创建文件夹及文件夹内容，详情见 1.2.1】</font>

> 📁 Library/<font color=gray>【如有需要手动创建文件夹及文件夹内容，详情见 1.2.1】</font>
>
> > 📁 Sdk/

> > 📃 Utils.php

> 📁 Model/<font color=blue>【如有需要根据 artisan 命令创建文件夹及文件夹内容，详情见 1.2.1】</font>

> > 📃 RouteServiceProvider.php<font color=red>【项目初始化完成后，根据业务逻辑调整代码，详情见 1.2.1】</font>

> 📁 Services/<font color=blue>【如有需要手动创建文件夹及文件夹内容，详情见 1.2.1】</font>

📁 bootstrap/

> 📃 app.php<font color=red>【项目初始化完成后，需要调整代码，详情见 1.2.1】</font>

📁 config/

> 📃 cache.php

> 📃 database.php

> 📃 key.php<font color=blue>【如有需要手动创建，详情见 1.2.1】</font>

> 📃 queue.php

> 📃 registry.php<font color=blue>【如有需要手动创建，详情见 1.2.1】</font>

> 📁 database/

> 📁 public/

> 📁 resources/

> 📁 views/

📁 routes/

📁 storage/

> 📁 app/
>
> > 📁 public/

> 📁 framework/

> 📁 logs/

📁 tests/

📁 vendor/

📃 .env

📃 .envdevelopment<font color=red>【手动创建，详情见 1.2.1】</font>

📃 .envpre<font color=red>【手动创建，详情见 1.2.1】</font>

📃 artisan

📃 composer.json<font color=blue>【如有需要 composer 工具添加依赖，详情见 1.2.1】</font>

📃 envmark.txt<font color=red>【手动创建，详情见 1.2.1】</font>

📃 phpunit.xml

#### 1.2.1 主目录说明及生成规范

- <font color=red>📃 bootstrap/app.php</font>、<font color=red>📃 .env</font>、<font color=red>📃 .envdevelopment</font>、<font color=red>📃 .envpre</font>及<font color=red>📃 envmark.txt</font>

  - 功能描述
    Laravel 最重要的环境变量配置
  - 使用方法
    项目初始化完成后首先创建`.envdevelopment`及`.envpre`文件;
    `.envdevelopment`是本地开发环境配置;`.envpre`是测试环境配置;`.env`是生产环境配置;
    为了区分不同的环境读取不同的配置文件需要配置`envmark.txt`并调整`app/bootstrap/app.php`文件代码;
    `envmark.txt`文件写入`production`表示读取`.env`配置;
    `envmark.txt`文件写入`development`表示读取`.envdevelopment`配置;
    `envmark.txt`文件写入`pre`表示读取`.envpre`配置;
    可参考配置<a href=https://quqi.com/6/295785 target=_blank>【`bootstrap/app.php`】</a><a href=https://quqi.com/6/295784 target=_blank>【`.env*`】</a>

- <font color=red>📃 config/registry.php</font>、<font color=red>📃 app/Providers/RouteServiceProvider.php</font>及<font color=red>📁 routes/</font>

  - 功能描述
    注册路由，用于分模块，可按照功能进行合理化拆分
  - 使用方法
    先配置`config/registry.php`和`app/Providers/RouteServiceProvider.php`;
    可参考配置<a href=https://quqi.com/6/295792 target=_blank>【`config/registry.php`】</a><a href=https://quqi.com/6/295791 target=_blank>【`app/Providers/RouteServiceProvider.php`】</a>
    然后在` routes/`配置路由文件，示例如下:
    📁 routes/

    > 📁 front/<font color=red>【按照业务分,前端项目(api-front.ledu.com)】</font>

    >

    > > 📁 floatingball/<font color=red>【按照功能模块分,悬浮球模块】</font>

    > > 📁 paycenter/<font color=red>【按照功能模块分,充值模块】</font>

    > > 📃 web.php

    > 📁 service/<font color=red>【按照业务分,后端项目(api-service.ledu.com)】</font>

    >

    > > 📁 ordercenter/<font color=red>【按照功能模块分,充值模块】</font>

    > > 📃 web.php

  在比如过有一个后台项目，那么可以在`routes/`下面建立个`admin`或`backend`之类的，对于简单的项目可以不必要配置的这么细，可以直接配置到`routes/web.php`里面，前面几步的配置可以省略

- <font color=red>📁 app/Http/Middleware/</font>、<font color=red>📃 app/Http/Kernel.php</font>及<font color=red>📁 routes/</font> + 功能描述
  配置路由中件，一般用于提供参数统一验证、请求合法性验证及接口登陆态验证等公共接口请求服务 + 使用方法
  添加中间件，示例如下(`app/Http/Middleware/CheckLeduLogin.php`):

  ````php
  namespace App\Http\Middleware;

      use App\Library\Sdk\LeduPassport\User;
      use App\Library\Utils;
      use Closure;

      class CheckLeduLogin
      {
      	/**
      	 * Handle an incoming request.
      	 *
      	 * @param  \Illuminate\Http\Request  $request
      	 * @param  \Closure  $next
      	 * @return mixed
      	 */
      	public function handle($request, Closure $next)
      	{
      		$callback = $request->has('callback') ? $request->get('callback') : "";
      		$ledu_user = User::instance();
      		$login_state = $ledu_user->isLogin();
      		if(!$login_state) Utils::errorExit($callback,'NOT_LOGIN','NOT LOGIN');
      		$commonparams = $request->get('commonparams')?:[];
      		$commonparams['ledu_user']['uid'] = $ledu_user->getUid();
      		$commonparams['ledu_user']['username'] = $ledu_user->getUserName();
      		$commonparams['ledu_user']['lastloginip'] = $ledu_user->getLastLoginIp();
      		$request->attributes->add([
      			'commonparams'=>$commonparams,
      		]);
      		return $next($request);
      	}
      }
      ```
      可参考配置<a href=https://quqi.com/6/295793 target=_blank>【`app/Http/Kernel.php`】</a>
      该配置中`$middleware`为公共中间件，`$middlewareGroups`为中间件组， `$routeMiddleware`为路由中间件；
      路由中间件使用示例如下(`routes/front/floatingball/api.php`):
      ```php
      Route::group(['namespace'=>'Api\Front\FloatingBall','middleware'=>['checkfrontparam','versiondispense','checkledulogin']],function() {
      		Route::group(['prefix' => 'init'], function () {
      			Route::any('/{version?}','InitController@init')->where('version','^v[0-9]+$');
      		});

  });
  ``` 其中`'middleware'=>['checkfrontparam','versiondispense','checkledulogin']`即为在`app/Http/Kernel.php`配置的路由中间件 + 针对跨域的路由配置
  可参考配置<a href=https://quqi.com/6/299641 target=_blank>【附件:Laravel 跨域路由配置】</a>

  ````

- <font color=blue>📁 app/Http/Controllers/</font>

  - 功能描述
    访问控制器
  - 使用方法
    尽量也按照功能模块拆分
    创建控制器示例如下:

  ```php
  php artisan make:controller Api/Front/FloatingBall/InitController
  ```

- <font color=blue>📁 app/Model/</font>

  - 功能描述
    数据库模型
  - 使用方法
    按照库名拆分，且必须建在`app/Model`下
    创建模型示例如下:

  ```php
  php artisan make:model Model/FloatingBall/Platform
  ```

- <font color=blue>📁 app/Services/</font>

  - 功能描述
    具体的业务逻辑
  - 使用方法
    在`app/Services`下创建服务类，可参考配置<a href=https://quqi.com/6/295794 target=_blank>【`app/Services/CommonService.php`】</a>

- <font color=blue>📁 app/Jobs/</font>

  - 功能描述
    队列脚本
  - 使用方法
    创建队列示例如下:

  ```php
  php artisan make:job Test
  ```

  生成的脚本文件目录为`app/Jobs/Test.php`

- <font color=blue>📁 app/Console/</font>

  - 功能描述
    存放 php 执行脚本，可用于执行定时任务
  - 使用方法
    - artisan 命令生成脚本模版
    ```bash
     artisan make:command Test
    ```
    - 生成的脚本文件目录为`app/Console/Commands/Test.php`
      可参考脚本<a href=https://quqi.com/6/295783 target=_blank>【模版】</a>
    - 脚本执行方法
    ```bash
     php artisan test
    ```
  - 使用规范
    - 定时任务
      尽量限定定时脚本执行时段，需要保留的日志存放到 storage/logs/文件夹下(链到挂载盘)
    ```bash
     */5 * 12 12 * /usr/local/php-7.1.8/bin/php /data/web/laravel/api-test.mujoy.com/artisan test --time=10 >> //data/web/laravel/api-test.mujoy.com/storage/logs/test.log
    ```

- <font color=blue>📁 verdor/</font>及<font color=blue>📃 composer.json</font>

  - 功能描述
    `verdor/`为依赖包文件所在目录，`composer.json`为依赖包更新配置
  - 使用方法
    添加依赖，示例如下:

  ```bash
  composer require lcobucci/jwt
  ```

  依赖包更新，示例如下:

  ```bash
  composer update
  ```

  具体的依赖包使用详见【1.3 依赖包安装使用规范】

- <font color=gray>📁 app/Library/</font>及<font color=gray>📃 confg/key.php</font>

  - 功能描述
    包含一些工具类及接口 Sdk
  - 使用方法
    先手动创建 Library 文件夹;
    Library 工具类可参考配置<a href=https://quqi.com/6/295795 target=_blank>【`Library/Utils.php`】</a>
    如果请求外部接口，先创建`Library/Sdk`目录，接口 sdk 继承`Library/Sdk/ApiBase.php`(参见<a href=https://quqi.com/6/295796 target=_blank>【`Library/Sdk/ApiBase.php`】</a>)；
    然后配置`confg/key.php`，可参考配置<a href=https://quqi.com/6/295797 target=_blank>【`confg/key.php`】</a>
    然后可以写接口 sdk 了，示例如下(`app/Library/LeduPassport/ApiPassport.php`)::

  ```php
  namespace App\Library\Sdk\LeduPassport;

  use App\Library\Sdk\ApiBase;
  use App\Library\Utils;

  class ApiPassport extends ApiBase
  {
  	protected $sdk_name = 'API_PASS';

  	private $request_params = [];

  	public function __construct($project='')
  	{
  		//init params
  		$this->request_params = [
  			'app_id'=>2,
  			'project'=>$project,
  			'rtime'=>microtime(true),
  			'req_time'=>time(),
  		];
  		$this->request_params['rid'] = Utils::createUuid(
  			explode(',', $this->request_params['rtime'])[0]
  		);
  		parent::__construct();
  	}

  	/**
  	 * 检查登录态
  	 * @param $token
  	 * @param $keep_login
  	 * @param string $ip
  	 * @return array|bool|float|int|mixed|\stdClass|string|null
  	 */
  	public function check_login_status($token,$keep_login,$ip=''){
  		$request_params = $this->request_params+[
  				'method'=>'check.loginstatus',
  				'token'=>$token,
  				'keep_login'=>$keep_login,
  				'ip'=>$ip?:Utils::getRealIp(),
  			];
  		return $this->make_request($request_params);
  	}

  	/**
  	 * 设置登录态缓存
  	 * @param $uid
  	 * @param $user_name
  	 * @param $password
  	 * @param $ip
  	 * @param $ua
  	 * @param $set_time
  	 * @param $keep_login
  	 * @return array|bool|float|int|mixed|\stdClass|string|null
  	 */
  	function set_login_status($uid,$user_name,$password,$ip,$ua,$set_time,$keep_login){
  		$request_params = $this->request_params+[
  				'method'=>'set.loginstatus',
  				'uid'=>$uid,
  				'user_name'=>$user_name,
  				'password'=>$password,
  				'ip'=>$ip,
  				'ua'=>$ua,
  				'time'=>$set_time,
  				'keep_login'=>$keep_login,
  			];
  		return $this->make_request($request_params);
  	}

  	/**
  	 * 删除登录态缓存
  	 * @param $token
  	 * @return array|bool|float|int|mixed|\stdClass|string|null
  	 */
  	public function delete_login_status($token){
  		$request_params = $this->request_params+[
  				'method'=>'del.loginstatus',
  				'token'=>$token,
  			];
  		return $this->make_request($request_params);
  	}

  	/**
  	 * 获取用户登陆的校验cookie
  	 * @param $username
  	 * @param $password
  	 * @param int $keep_login
  	 * @param string $ip
  	 * @param $ua
  	 * @return array|bool|float|int|mixed|\stdClass|string|null'
  	 */
  	function login($username,$password,$keep_login=0,$ip='',$ua=''){
  		$request_params = $this->request_params+[
  				'method'=>'user.login',
  				'username'=>$username,
  				'password'=>md5(md5($password).$this->api_constants['KEY']),
  				'keep_login'=>$keep_login,
  				'ip'=>$ip?:Utils::getRealIp(),
  				'ua'=>$ua?:Utils::getUa(),
  			];
  		return $this->make_request($request_params);
  	}

  	/**
  	 * 获取用户信息
  	 * @param $username
  	 * @param bool $is_username
  	 * @return array|bool|float|int|mixed|\stdClass|string|null
  	 */
  	function info($username,$is_username=true){
  		$request_params = $this->request_params+[
  				'method'=>'user.info',
  			];
  		if($is_username){
  			$request_params['username'] = $username;
  		}else{
  			$request_params['uid'] = $username;
  		}
  		return $this->make_request($request_params);
  	}
  }
  ```

### 1.3 依赖包安装使用规范

<font color=red>⚠️ 依赖包不允许手动引入使用</font>

- 本地源配置(`composer.json`)

  ```php
  "repositories": {
  		"packagist": {
  			"type": "composer",
  			"url": "https://mirrors.aliyun.com/composer/"
  		},
  		"local": {
  			"type": "vcs",
  			"url": "https://gitlab.mjutech.com/vendor/netdata.git"
  		}
  	}
  ```

- 常用依赖包引入
  - miaoju-auth 登陆
  ```bash
  	composer require mjutech/netdata
  ```

### 1.4 项目代码提交管理规范

- git 分支管理
  主仓库必须要有 pre 分支，测试环境用此分支代码提交;个人仓库尽量按照版本建立开发分支
  使用示例:

```bash
git checkout -b dev20201212
```
