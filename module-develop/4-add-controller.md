# 4. 添加控制器

**/modules/custom/hello\_world/src/Controller/HelloController.php**

```
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



