## 推广跟踪API接口


> 推广链接参数接收

比如广告主推广着陆页为
```
http://www.game123.com/portal/37
```

联盟后台广告设置着陆页为
```
http://www.game123.com/portal/37?h={tid}
```

点击广告时 {tid} 会被替换为跟踪字符串, 比如 

```
http://www.abc.com/portal/37?h=f38ffb9dcac975380fc8e85e02389b6d3ef7ebd0536a3609f477a6f8868f12675d82f
```

字符串长度不超过2K

> 跟踪回传接口参数

| 参数        | 说明           | 参数格式  | 必须 |
| ------------- |:-------------:| -----:|---|
| h     | 广告连接传递过来的跟踪字符串 | String | 是 |
| s      | 加密签名      |   32位小写md5值 | 是 |
| uuid      | 唯一ID防止重复提交      |   String | 是 |
| amount      | 效益金额(字符串表示的浮点数)      |   String | 否 |
| e      | 附加信息      |   String | 否 |

```
返加ok表示成功, 其它指错误
```

> 加密签名算法

```
s = md5(h+uuid+amount+e+accessKey)
```
> 代码示例
Python:
```python
import md5
if __name__ == "__main__":
    h = "f38ffb9dcac975380fc8e85e02389b6d3ef7ebd0536a3609f477a6f8868f12675d82f04b61a7ad"
    uuid = "1234567"
    e = "Register but not charge"
    amount="0.98"
    accessKey = "your accessKey"
    print "http://cc.xaepgyy.com/track?h=%s&s=%s&info=%s&uuid=%s&amount=%s" % (h, md5.md5(h+uuid+amount+e+accessKey).hexdigest(), e, uuid, amount)
```

PHP:
```php
<?php
    $h = "f38ffb9dcac975380fc8e85e02389b6d3ef7ebd0536a3609f477a6f8868f12675d82f04b61a7ad";
    $uuid = "1234567";
    $e = "Register but not charge";
    $amount="0.98";
    $accessKey = "your accessKey";
    printf("http://cc.xaepgyy.com/track?h=%s&s=%s&info=%s&uuid=%s&amount=%s", $h, md5($h.$uuid.$amount.$e.$accessKey), $e, $uuid, $amount)
?>
```

