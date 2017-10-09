# [6. 渲染系统](/module-develop/6-render.md)6. 渲染系统

[https://www.drupal.org/docs/8/api/render-api](https://www.drupal.org/docs/8/api/render-api)

Drupal的渲染系统大概由两个部份组成:

1. 渲染管线----支持常见格式\(HTML,json,以及其它\)
2. 渲染数组----它用于呈现一个HTML页面。允许它们嵌套\(像HTML\)和修改\(Drupal是高定制的\)。

Drupal通过渲染系统将用户的请求转换成HTML响应传送给用户，Drupal的渲染系统涉及到缓存以及Symfony的一些知识，其结构比较复杂。本章将详细讨论其细节。

6.1 渲染数组与缓存

6.2 可冒泡的元数据

6.3 自动占位符

6.4 Drupal 8 渲染管线

6.5 渲染数组

