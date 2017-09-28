# 5. 添加路由文件.routing.yml

在你的模块根文件夹中，添加一个新文件"**hello\_world.routing.yml**"添加一下内容:

**/modules/custom/hello\_world/hello\_world.routing.yml**

```
hello_world.content:
  path: '/hello'
  defaults:
    _controller: '\Drupal\hello_world\Controller\HelloController::content'
    _title: 'Hello World'
  requirements:
    _permission: 'access content'
```

请注意，您在模块的路由表中保留的空间，第一行中的“hello\_world” 不一定是您为模块选择的机器名称。但是，为了在您的路由和菜单文件中保持一致，这是一个最佳做法。当添加菜单链接时，将在下一节中使用完整的条目名称，将该链接连接到此路由表条目中。hello\_world.contenthello\_world.content

如果您已经将模块激活了，您将需要从用户界面清除站点的缓存或使用drush。如果没有，请继续激活它。admin/config/development/performancedrush cache-rebuilddrush cr

