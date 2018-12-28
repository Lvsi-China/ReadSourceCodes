入口文件：public/index.php


```php
// 开始计时
define('LARAVEL_START', microtime(true));

// 引入 composer 的自动加载文件
require __DIR__ . '/../vendor/autoload.php';

// 正式启动 Larvel，生成一个指代整个项目工程的 app 全局对象
$app = require_once __DIR__ . '/../bootstrap/app.php';

// 通过全局对象 app 的构造对象的 make 方法创建一个 Kernel 核心对象
$kernel = $app->make(Illuminate\Contracts\Http\Kernel::class);

/*-------------这部分是整个 ->请求->响应-> 周期----------------*/

// 获取当前的请求快照 , 然后赋给全局对象 $request.
// 将 $request 传入 $kernel , 开始处理这个请求.
// 请求处理完成之后 , 将结果封装成一个【响应对象】并赋给 $response
$response = $kernel->handle(
    $request = Illuminate\Http\Request::capture()
);

// $response 将响应结果返回
$response->send();

// 内核停止
$kernel->terminate($request, $response);

/*-------------这部分是整个 ->请求->响应-> 周期----------------*/

```