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

git clone --branch 8.x-1.x [https://git.drupal.org/project/composer\_manager.git](https://git.drupal.org/project/composer_manager.git)

#### 2. 安装composer\_manager模块

#### 3. 进入到composer\_manager目录，执行脚本

php scripts/init.php

![](/assets/8.png)

#### 4. 在Drupal目录的根目录运行composer drupal-update

composer drupal-update





### 在composer.json中定义一个依赖

你可以在composer.json文件中为模块定义外部依赖。Drupal核心不会自动地发现并管理这些依赖。为了利用composer.json文件中定义的依赖，你需要使用以下维护方式:

1. 使用composer安装Drupal核心以及模块
2. 在Drupal安装的根目录下手工修改composer.json文件



