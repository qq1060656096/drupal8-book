# 8. 添加css和js

### **1.在模块根目录下创建hello\_world.libraries.yml**文件

**/modules/custom/hello\_world/hello\_world.libraries.yml**

```
hello_world:
  version: 1.x
  css:
    theme:
      css/hello_world_module_test.css: {}
  js:
    js/hello_world_module_test.js: {}
```

### 2**. 添加css和js文件**

**/modules/custom/hello\_world/css/hello\_world\_module\_test.css**

```
.hello_world{
    color: red;
}
```

**/modules/custom/hello\_world/css/hello\_world\_module\_test.js**

```
alert('hello_world_module_test.js');
```

### 3. 在twig模板中附加一个外部js和css库

**{{ attach\_library\('hello\_world/hello\_world'\) }}**

**{{ attach\_library\('模块名/库名'\) }}**

**/modules/custom/hello\_world/templates/my-template.html.twig**

```
{#
/**
* @file
* Default theme implementation to print Lorem ipsum text.
*
* Available variables:
* - source_text
*
* @see template_preprocess_loremipsum()
*
* @ingroup themeable
*/
#}
{{ attach_library('hello_world/hello_world') }}
<div class="hello_world">
    {% for item in source_text %}
        <p>{{ item }}</p>
    {% endfor %}
</div>
```

### 6.访问页面
http://domain/custom-template




