# 4. 添加composer.json文件

这里我们使用一个github上身份证解析库做演示

[https://github.com/qq1060656096/Cards.git](https://github.com/qq1060656096/Cards.git)

### 1 添加composer.json文件

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

### 2 安装composer\_manager模块

[https://www.drupal.org/project/composer\_manager/git-instructions](https://www.drupal.org/project/composer_manager/git-instructions)



#### 1. 使用git下载代码

git clone --branch 8.x-1.x https://git.drupal.org/project/composer\_manager.git

####  2. 进入到composer\_manager目录

cd composer\_manager

#### 3. 执行脚本

php scripts/init.php



