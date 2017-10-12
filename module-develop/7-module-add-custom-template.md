# 7. 从自定义模块创建自定义模板

hook\_theme

此钩子声明的实现将指定特定渲染数组如何渲染为HTML。

[https://api.drupal.org/api/drupal/core!lib!Drupal!Core!Render!theme.api.php/function/hook\_theme/8.4.x](https://api.drupal.org/api/drupal/core!lib!Drupal!Core!Render!theme.api.php/function/hook_theme/8.4.x)



在模块根目录下templates模板文件夹的内部创建twig模板。文件的名称必须与您所输入的内容相匹配,文件名将是my-template.html.twig。以下是我用来测试的文件：hook\_theme\(\)

这样做的好处是，如果您的主题中不存在这样的文件，模块中定义的模板文件将被使用。只需将文件转储到主题的/templates文件夹中，清除缓存缓存，它就会读取该文件。



