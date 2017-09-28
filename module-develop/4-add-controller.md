# 4. 添加控制器

为了响应hello world模块页面的请求，你需要添加一个控制器，用来告诉当请求到来时，模块要做什么事。

在你模块目录中，你应该创建符合PSR-4标准的目录结构/src/Controller，并在该目录下创建控制器文件HelloController.php。

我们这个模块只是想输出hello world这样的字符串，需要在/src/Controller/HelloController.php文件中输入以下代码:

**/modules/custom/hello\_world/src/Controller/HelloController.php**

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

}
```



