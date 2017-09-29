# 6. 添加菜单链接

在你的模块根文件夹中，添加一个新文件"**hello\_world.links.menu.yml**"添加一下内容:

**/modules/custom/hello\_world/hello\_world.links.menu.yml**

```
hello_world.admin:
  title: 'Hello module settings'
  description: 'example of how to make an admin settings page link'
  parent: system.admin_config_development
  route_name: hello_world.content
  weight: 100
```



