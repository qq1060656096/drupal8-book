# 7. 从自定义模块创建自定义模板

hook\_theme

此钩子声明的实现将指定特定渲染数组如何渲染为HTML。

[https://api.drupal.org/api/drupal/core!lib!Drupal!Core!Render!theme.api.php/function/hook\_theme/8.4.x](https://api.drupal.org/api/drupal/core!lib!Drupal!Core!Render!theme.api.php/function/hook_theme/8.4.x)

在模块根目录下templates模板文件夹的内部创建twig模板。文件的名称必须与您所输入的内容相匹配,文件名将是my-template.html.twig。以下是我用来测试的文件：hook\_theme\(\)

这样做的好处是，如果您的主题中不存在这样的文件，模块中定义的模板文件将被使用。只需将文件转储到主题的/templates文件夹中，清除缓存缓存，它就会读取该文件。

### **1.在模块根目录下创建templates目录，这个目录用于存放定义的twig模板文件my-template.html.twig**

### /modules/custom/hello\_world/templates/my-template.html.twig

```
{#
/**
 * @file
 * Default theme implementation to print Lorem ipsum text.
 *
 * Available variables:
 *   - source_text
 *
 * @see template_preprocess_loremipsum()
 *
 * @ingroup themeable
 */
#}
<div class="hello_world">
    {% for item in source_text %}
        <p>{{ item }}</p>
    {% endfor %}
</div>
```

### **2.接下来，在/modules/custom/hello\_world/src/Controller/HelloController.php类中添加customTemplate\(\)方法           **

```php
/**
 * 创建自定义模板
 */
public function customTemplate()
{
    return [
        '#theme' => 'my_test',
        '#source_text' => [
            'hello_world模块',
            $this->t('Test Value')
        ],
    ];
}
```

### **3. 为了能访问这一个页面，我们将会在模块目录下创建一个路由文件\(hello\_world.routing.yml\)。在文件中定义一个路由来通知Drupal使用显示我们的页面。代码如下:**

```markdown
hello_world.custom-template:
  path: '/custom-template'
  defaults:
    _title: '自定义模块中创建自定义模板'
    _controller: '\Drupal\hello_world\Controller\HelloController::customTemplate'
  requirements:
    _access: 'TRUE'
```

### **4.清空缓存**

### **5.访问页面**

[http://domain/custom-template](https://www.gitbook.com/book/qq1060656096/drupal8-book/edit#)

![](/assets/12.png)

### 演示代码文件

/modules/custom/hello\_world/src/Controller/HelloController.php

```php
<?php
namespace Drupal\hello_world\Controller;

use Drupal\Core\Controller\ControllerBase;

/**
 * Class HelloController
 * @package Drupal\hello_world\Controller
 */
class HelloController extends ControllerBase {

    /**
     * Display the markup.
     *
     * @return array
     */
    public function content() {
        return array(
            '#type' => 'markup',
            '#markup' => $this->t('Hello, World!'),
        );
    }

    /**
     * 创建自定义模板
     */
    public function customTemplate()
    {
        return [
            '#theme' => 'my_test',
            '#source_text' => [
                'hello_world模块',
                $this->t('Test Value')
            ],
        ];
    }
}
```

/modules/custom/hello\_world/templates/my-template.html.twig

```
{#
/**
 * @file
 * Default theme implementation to print Lorem ipsum text.
 *
 * Available variables:
 *   - source_text
 *
 * @see template_preprocess_loremipsum()
 *
 * @ingroup themeable
 */
#}
<div class="hello_world">
    {% for item in source_text %}
        <p>{{ item }}</p>
    {% endfor %}
</div>
```

/modules/custom/hello\_world/hello\_world.routing.yml

```markdown
hello_world.content:
  path: '/hello'
  defaults:
    _controller: '\Drupal\hello_world\Controller\HelloController::content'
    _title: 'Hello World'
  requirements:
    _permission: 'access content'
hello_world.form:
  path: '/hello-example-form'
  defaults:
    _title: 'Example form'
    _form: '\Drupal\hello_world\Form\ExampleForm'
  requirements:
    _access: 'TRUE'
hello_world.custom-template:
  path: '/custom-template'
  defaults:
    _title: '自定义模块中创建自定义模板'
    _controller: '\Drupal\hello_world\Controller\HelloController::customTemplate'
  requirements:
    _access: 'TRUE'
```



