# 创建.info.yml文件,让drupal识别你的模块

info.yml文件是drupal8 模块、主题、安装配置必须的文件，它提供了一个扩展\(Extend\)的基本信息描述  
。主要包括模块、主题、安装配置，为用户管理界面提供信息，版本兼容性，以及其它的一些信息。

### hello world模块的信息文件

在hello world模块的根目录创建一个"**hello\_world.info.yml**"文件,并输入以下内容就drupal8就可以识别你的模块了:

#### /modules/custom/hello\_world/hello\_world.info.yml

```
name: Hello World Module
description:  Creates a page showing “Hello World”。
package: Custom
type: module
core: 8.x
```

登录drupal8后台管理，点击**Extend**菜单进入模块列表，在搜索框中输入hello就搜索模块了

![](/assets/2.png)

