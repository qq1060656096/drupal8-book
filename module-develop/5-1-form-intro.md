# 5.1 表单介绍

表单类实现\Drupal\Core\Form\FormInterface和一种形式的基本工作是由定义buildForm，validateForm和submitForm接口的方法。当请求表单时，

它被定义为通常称为Form API数组或简单$form数组的可渲染数组。该$form数组由渲染过程转换为HTML，并显示给最终用户。

当用户提交表单时，请求将发送到表单所显示的相同URL，Drupal会在请求中注意到传入的HTTP POST数据，

而不是构建表单并将其显示为HTML构建表单，然后继续调用适用的验证和提交处理程序。



将表单定义为结构化数组而不是直接HTML具有许多优点，包括：

1. 所有表单的HTML输出一致。

2. 一个模块提供的表单可以轻松地被另一个模块更改，而无需复杂的搜索和替换逻辑

3. 诸如文件上传和投票小部件的复杂表单元素可以封装在可重复使用的包中，包括显示和处理逻辑。

4. Drupal中常用的形式有几种。每个都有一个基类，您可以在自己的自定义模块中扩展。



Drupal中常用的表单有几种。每个都有一个基类，您可以在自己的自定义模块中扩展。



首先，确定您需要构建的表单类型：

首先，确定您需要构建的表单类型：



1. 一般的表单，继承FormBase。

2. 一个配置表单，使管理员可以更新模块的设置。继承ConfigFormBase。

3. 用于删除提供确认步骤的内容或配置的表单。继承ConfirmFormBase。

FormBase实现FormInterface，并且ConfigFormBase和ConfirmFormBase都扩展了FormBase，因此扩展这些类的任何表单都必须实现一些必需的方法。



所需方法



FormBase实现FormInterface，因此FormBase需要其层次结构中的任何形式来实现几种方法：



* getFormId\(\)
* buildForm\(\)
* validateForm\(\)
* submitForm\(\)
* getFormId\(\)



getFormId\(\)

public function getFormId\(\)

这需要返回一个字符串，该字符串是表单的唯一ID。根据模块的名称命名空格。

例：

```php
public function getFormId() {
    return 'mymodule_settings';
}
```

buildForm\(\)

public function buildForm\(array $form, FormStateInterface $form\_state\)

这返回一个Form API数组，它定义了您的窗体所构成的每个元素。

例：

```php
public function buildForm(array $form, FormStateInterface $form_state) {
    $form['phone_number'] = array(
        '#type' => 'tel',
        '#title' => 'Example phone',
     );
     return $form;
}
```

验证表单

用户填写表单并单击提交按钮后，通常要对正在收集的数据执行某种验证。为了使用Drupal的Form API，我们只需在ExampleForm类中的\ Drupal \ Core \ Form \ FormInterface中实现validateForm方法。



来自表单的用户提交的值包含在$ form\_state-&gt; getValue（'field\_id'）的$ form\_state对象中，其中'field\_id'是将Form元素添加到FormExample :: buildForm（）中的$ form数组时使用的关键字， 。我们可以对此值进行自定义验证。如果您需要获取所有提交的值，可以使用$ form\_state-&gt; getValues（）来实现。



表单验证方法可以使用所需的任何PHP处理来验证该字段是否包含所需的值，并在其为无效值的情况下引发错误。在这种情况下，由于我们扩展了\Drupal\Core\Form\FormBase类，我们可以使用\Drupal\Core\Form\FormStateInterface::setErrorByName\(\)在特定的表单元素上注册错误，并提供一个相关的消息，错误。

当表单被提交并且Drupal执行它自己和验证所有在过程中注册的错误被收集时，表单的HTML被重建，并且突出显示带有错误的字段。这允许用户更正任何错误并重新提交表单。

以下是一个简单的validateForm\(\)方法的示例：

```php
/**
 * {@inheritdoc}
 */
public function validateForm(array &$form, FormStateInterface $form_state) {
  if (strlen($form_state->getValue('phone_number')) < 3) {
    $form_state->setErrorByName('phone_number', $this->t('The phone number is too short. Please enter a full phone number.'));
  }
}
```

如果在表单验证期间没有注册错误，那么Drupal会继续处理表单。在这一点上，假设值是有效的，并且可以以我们的模块需要使用数据的任何方式进行处理和使用。$form\_state-&gt;getValues\(\)



提交表格/处理表格数据

最后，我们准备好使用我们收集的数据，并将其保存到数据库或发送电子邮件或任何其他操作。为了使用Drupal的Form API，我们需要从我们的类中实现submitForm方法。\Drupal\Core\Form\FormInterfaceExampleForm

就像上面的验证方法一样，在提交表单时从用户收集的值都在，在这一点上，我们可以假设它们已经过验证，并且可以供我们使用。访问我们的'phone\_number'字段的值可以通过访问来完成。$form\_state-&gt;getValues\(\)$form\_state-&gt;getValue\('phone\_number'\)



以下是一个简单的submitForm方法的示例，它使用以下方式显示页面上'phone\_number'字段的值：drupal\_set\_message\(\)

```php
/**

* {@inheritdoc}

*/

public function submitForm(array &$form, FormStateInterface $form_state) {
    drupal_set_message($this->t('Your phone number is @number', array('@number' => $form_state->getValue('phone_number'))));
}
```

这是处理提交的表单数据的一个非常简单的例子。对于更复杂的例子来看看扩展FormBase在核心的一些类。





