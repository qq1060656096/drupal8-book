# 8.1 直接在twig模板中添加css和js

### 1. 在模块根目录下创建hello\_world.libraries.yml文件

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

### 2. 添加css和js文件

**/modules/custom/hello\_world/css/hello\_world\_module\_test.css**

```css
.hello_world{
    color: red;
}
```

**/modules/custom/hello\_world/css/hello\_world\_module\_test.js**

```js
alert('hello_world_module_test.js');
```

### 3. 在twig模板中附加一个外部js和css库

**/modules/custom/hello\_world/templates/my-template.html.twig**

```markdown
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
        <p>
            {{ item }}
        </p>
    {% endfor %}
</div>
```

### 4. 清空缓存

### 5. 访问页面

[http://domain/custom-template](http://domain/custom-template)

![](/assets/13.png)

