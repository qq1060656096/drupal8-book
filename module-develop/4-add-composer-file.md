# 4. 添加composer.json文件

这里我们使用一个github上身份证解析库做演示

https://github.com/qq1060656096/Cards.git





在你的模块根文件夹中，添加一个新文件"composer.json"添加一下内容:

```
{
    "name": "drupal/hello_world",
    "description": "这是一个示例模块",
    "type": "drupal-module",
    "repositories": [
        {
            "type": "vcs",
            "url": "https://github.com/qq1060656096/Cards.git"
        }
    ],
    "require": {
        "wei/cards": "~1"
    }
}
```



