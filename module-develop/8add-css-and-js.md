# 8. 添加css和js

[https://www.drupal.org/docs/8/creating-custom-modules/adding-stylesheets-css-and-javascript-js-to-a-drupal-8-module](https://www.drupal.org/docs/8/creating-custom-modules/adding-stylesheets-css-and-javascript-js-to-a-drupal-8-module)

1. 直接在twig模板中添加css和js
2. 在所有页面或一部分页面添加css和js
3. 在预处理功能中点击css和js

### 1.直接在twig模板中添加css和js

```
{{ attach_library('your_module/library_name') }}
```

1. 在渲染数组中添加css和js

```php
 return [
   '#theme' => 'your_module_theme_id',
   '#someVariable' => $some_variable,
   '#attached' => array(
     'library' => array(
       'your_module/library_name',
     ),
   ),
 ];
```

### 2.在所有页面或一部分页面添加css和js

hook\_page\_attachments\(\)

[https://api.drupal.org/api/drupal/core!lib!Drupal!Core!Render!theme.api.php/function/hook\_page\_attachments/8.5.x](https://api.drupal.org/api/drupal/core!lib!Drupal!Core!Render!theme.api.php/function/hook_page_attachments/8.5.x)

```php
// From core/modules/contextual/contextual.module.
function contextual_page_attachments(array &$page) {
  if (!\Drupal::currentUser()->hasPermission('access contextual links')) {
    return;
  }

  $page['#attached']['library'][] = 'contextual/drupal.contextual-links';
}
```

### 3.在预处理功能中点击css和js

hook\_preprocess\_HOOK

[https://api.drupal.org/api/drupal/core!lib!Drupal!Core!Render!theme.api.php/function/hook\_preprocess\_HOOK/8.5.x](https://api.drupal.org/api/drupal/core!lib!Drupal!Core!Render!theme.api.php/function/hook_preprocess_HOOK/8.5.x)

```php
function fluffiness_preprocess_maintenance_page(&$variables) {
  $variables['#attached']['library'][] =  'fluffiness/cuddly-slider';
}
```

## 定义资源库

要定义一个或多个（资产）库，请将文件添加到模块文件夹的根目录（与.info.yml文件一起）。（如果您的模块被命名，则文件名应为）。该文件中的每个“库”都是详细介绍CSS和JS文件（资产）的条目，如下所示：\*.libraries.yml fluffiness fluffiness.libraries.yml

```
cuddly-slider:
  version: 1.x
  css:
    layout:
      css/cuddly-slider-layout.css: {}
    theme:
      css/cuddly-slider-theme.css: {}
  js:
    js/cuddly-slider.js: {}
```

您可能会注意到对于js不存在的css的“layout”和“theme”键。这表示css文件所属的样式类型。

您可以CSS使用5种不同级别的样式设置权重：

base：CSS重置/标准化加HTML元素样式。键分配一个重量CSS\_BASE = -200

layout：网页的宏布置，包括任何网格系统。键分配一个重量CSS\_LAYOUT = -100

component：离散的，可重复使用的UI元素。键分配一个重量CSS\_COMPONENT = 0

state：处理客户端更改组件的样式。键分配一个重量CSS\_STATE = 100

theme：组件的纯视觉造型（“外观感”）。键分配一个重量CSS\_THEME = 200



这是由SMACSS标准定义的。所以这里如果你指定主题，这意味着CSS文件包含与主题相关的样式，这是纯粹的外观和感觉。更多信息在这里。您不能使用其他键，因为这些将导致严格的警告。

此示例假定实际的JavaScript 位于模块的子文件夹中。你也可以让JS来自外部URL，包括CSS文件，还有其他的可能性。有关详细信息，请参阅CDN /外部托管库。cuddly-slider.jsjs

但是，请记住，Drupal 8默认情况下不再在所有页面上加载jQuery; Drupal 8只加载必要的东西。因此，我们必须声明我们的模块的库声明对包含jQuery 的库的依赖。它既不是模块也不是提供jQuery的主题，它是Drupal核心：是我们要声明的依赖关系。（这是一个扩展名，后跟一个斜杠，后跟图书馆名称，所以如果一些其他图书馆想依赖我们的图书馆，那么就必须声明一个依赖关系，因为它是我们模块的名称。）cuddly-slidercore/jquerycuddly-sliderfluffiness/cuddly-sliderfluffiness



所以，为了确保jQuery可用，我们将以上更新为：js/cuddly-slider.js

```
cuddly-slider:
  version: 1.x
  css:
    theme:
      css/cuddly-slider.css: {}
  js:
    js/cuddly-slider.js: {}
  dependencies:
    - core/jquery
```

按照您的预期，列出CSS和JS资产的顺序也是它们将被加载的顺序。

