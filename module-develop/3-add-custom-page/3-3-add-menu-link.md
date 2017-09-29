# 3.3 添加菜单链接

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

**您已经将模块激活了，您将需要从用户界面清除站点的缓存或使用drush。如果没有，请继续激活它。admin/config/development/performance**

**drush cache-rebuilddrush cr**

这将会在管理配置页面添加一个链接，该链接引用hello\_world.content的路由信息，需要清空缓存已使配置生效。清空缓存后，在管理配置页面开发部份将会看到”Hello module settings”菜单链接，单击这个链接，系统调用hello\_world模块。

![](/assets/7.png)

**附加提示  
**

该文件非常灵活。您还可以使用它链接到外部资源，或通过路径链接：.links.menu.yml

```
hello_world.admin:
  title: 'Hello module settings'
  description: 'example of how to make an admin settings page link'
  parent: system.admin_config_development
  url: http://example.com/this-is-some-example
  weight: 100
hello_world.admin2:
  title: 'Hello module settings'
  description: 'example of how to make an admin settings page link'
  parent: system.admin_config_development
  url: internal:/some-internal-path
```



