<h1 align="center">Easy SMS 梦网云通信企业网关</h1>

## 安装

```shell

$ composer require "zacksleo/easy-sms-mw"

```

## 通过自定义网关使用

```php

use Overtrue\EasySms\EasySms;
use zacksleo\easysms\Gateways\MwGateway;

$config = [
    ...
    'default' => [
        'gateways' => [
            'mw', // 配置自定义网关
        ],
    ],
    'gateways' => [
        'mw' => [
            'userId' => 'your-api-key',
            'password' => 'your-api-password',
            'pszSubPort' => 'psz-sub-port',
        ],
    ],
];

$easySms = new EasySms($config);

// 注册
$easySms->extend('mw', function($gatewayConfig){
    // $gatewayConfig 来自配置文件里的 `gateways.mygateway`
    return new MwGateway($gatewayConfig);
});

$res = $easySms->send(13188888888, [
    'content'  => '您的验证码为: 6379',
]);

if ($res['mw']['status'] == 'success') {
    throw new Exception('发送失败');
}
```

> 更多内容请参考：[easy-sms 文档](https://github.com/overtrue/easy-sms)
