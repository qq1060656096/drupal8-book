# 8. 添加css和js

https://www.drupal.org/docs/8/creating-custom-modules/adding-stylesheets-css-and-javascript-js-to-a-drupal-8-module

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

https://api.drupal.org/api/drupal/core%21lib%21Drupal%21Core%21Render%21theme.api.php/function/hook\_page\_attachments/8.5.x

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

https://api.drupal.org/api/drupal/core%21lib%21Drupal%21Core%21Render%21theme.api.php/function/hook\_preprocess\_HOOK/8.5.x

```php
function fluffiness_preprocess_maintenance_page(&$variables) {
  $variables['#attached']['library'][] =  'fluffiness/cuddly-slider';
}
```



