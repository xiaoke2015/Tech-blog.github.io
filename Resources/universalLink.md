# Universal Link


## 背景介绍

微信开发者平台，包括QQ目前新建应用都必须配置Universal Link，老本版存量问题，微信开发者平台公告2020年3月起逐渐收回老版本功能。因此更新SDK配置Universal Link
就是必须要做的。

## 自己配置的Universal Link

1. 让后台人员准备一个https的链接，供后面存放建好的apple-app-site-association文件

2. 制作apple-app-site-association文件，并放置在准备好的链接根目录下

3. 在App Store对相应的buildID开启Universal Link服务

4. 在Xcode开启Associated Domains，并填写对应Domains

5. 用GET请求测试该链接下的文件内容，并在safari浏览器中测试

## 配置详解

1. 准备htttps链接，制作apple-app-site-association文件（文件名一定吧不能更改），放根目录的（.well-known）的子目录下，或者根目录下，地址一定是这两个中的一个。

2. 制作apple-app-site-association文件

    a.单个app,示例如下，其实就是一个json，apps数组不用管，details里面填入对应得appID和paths。appID就是用前缀+bundleID的方式，把它交给你的后台人员，按照之前说的放到相应目录。并且使用GET请求进行测试，确保路径能正常访问。

    ```
    {
    "applinks": {
            "apps": [],
            "details": [
                {
                    "appID": "xxxxxxxx.com.xxxxxxx",
                    "paths": ["*"]
                },
            ]
        }
    }
    ```

    b.多个App同时用1个apple-app-site-association，示例如下，通过paths来限制打开那个应用。其他同单个单用,打开app就是前面域名+/shahxi/

    ```
    {
    "applinks": {
            "apps": [],
            "details": [
                {
                    "appID":  "xxxxxxxx.com.xxxxxxx",
                    "paths": ["/shanxi/*"]
                },

                {
                    "appID":  "xxxxxxxx.com.xxxxxxx",
                    "paths": ["/chengdu/*"]

                },
            ]
        }
    }
    ```


## 参考文档

* [微信 文档](https://developers.weixin.qq.com/doc/oplatform/Mobile_App/Access_Guide/iOS.html)

* [apple 文档](https://developer.apple.com/documentation/safariservices/supporting_associated_domains)

