# 6.4 Drupal 8 渲染管线

[https://www.drupal.org/docs/8/api/render-api/the-drupal-8-render-pipeline](https://www.drupal.org/docs/8/api/render-api/the-drupal-8-render-pipeline)

### 高级别: 控制器、视图事件和主要内容渲染

![](/assets/11.png)

### 路线

1. 控制器返回Response对象的路由绕过下面的管道。他们直接依靠Symfony渲染管道。

   相当于直接输出内容

1. 控制器返回“主要内容”作为渲染数组的路由自动具有以多种方式被请求的能力：它可以以某种格式（HTML，JSON ...）和/或以某种装饰方式呈现（例如，使用块围绕主要内容）。

### 管道

```
这可以被认为是Drupal渲染管道，但它真的只是嵌入在Symfony渲染管道中。



1. 控制器返回一个渲染数组后，VIEW 事件将被触发HttpKernel，因为控制器的结果不是一个Response，而是一个渲染数组。

2. MainContentViewSubscriber已订阅该VIEW事件。它检查控制器结果是否是一个渲染数组，如果是这样，它保证生成一个Response。

3. 接下来，MainContentViewSubscriber检查是否支持协商的请求格式：

    存在主内容呈现器服务的任何格式（MainContentRendererInterface支持实现。

    如果不支持协商的请求格式，则会生成406个JSON响应，该响应以机读方式列出支持的格式（根据RFC 2616 10.4.7节）。

4. 否则，当协商的请求格式被支持时，相应的主内容渲染器服务被初始化。通过调用服务生成响应。而已！MainContentRendererInterface::renderResponse\(\)
```

### 主要内容渲染器

```
每个主要内容渲染器服务都可以选择如何实现renderResponse\(\)方法。当然，它可以选择添加受保护的帮助方法来提供更多的结构，如果它是一个复杂的主要内容渲染器。



Drupal 8提供以下主要内容呈现（并因此支持以任何格式/ MIME类型之一渲染任何渲染数组）：

    HTML: HtmlRenderer \(text/html\)

    AJAX: AjaxRenderer \(application/vnd.drupal-ajax\)

    Dialog: DialogRenderer \(application/vnd.drupal-dialog\)

    Modal: ModalRenderer \(application/vnd.drupal-modal\)
```

### HTML内容渲染器

1. HtmlRenderer::prepare\(\)接收主要内容渲染，并确保我们有一个渲染数组'\#type' =&gt; 'page'（对应于&lt;body&gt;）：

   1. 如果主要内容呈现数组已经存在'\#type' =&gt; 'page'，那么我们就完成了。

   2. 否则，我们需要构建'\#type' =&gt; 'page'渲染数组。该RenderEvents::SELECT\_PAGE\_DISPLAY\_VARIANT事件被分派，选择页面显示变体。

      默认SimplePageVariant使用，不适用任何装饰。[https://api.drupal.org/api/drupal/core!lib!Drupal!Core!Render!Plugin!DisplayVariant!SimplePageVariant.php/class/SimplePageVariant/8.2.x](https://api.drupal.org/api/drupal/core!lib!Drupal!Core!Render!Plugin!DisplayVariant!SimplePageVariant.php/class/SimplePageVariant/8.2.x)

      但是，当启用块模块时，BlockPageVariant将使用该模块，这允许站点构建器在任何页面区域中放置块，因此“decorate”主要内容。

      Drupal 8模块也可以订阅此事件，并使用不同的页面变体，即使在每个路由的基础上。（面板，页面管理器等可以干净地实现，由于这个事件。）

2. HtmlRenderer::prepare\(\)现在保证在一个渲染'\#type' =&gt; 'page'数组上工作。并被hook\_page\_attachments\(\)和hook\_page\_attachments\_alter\(\)调用。（用于附加不属于特定页面的页面级资源。）

3. HtmlRenderer::renderResponse\(\)使用上一步返回的渲染'\#type' =&gt; 'page'数组并将其'\#type' =&gt; 'html'包装起来。并被hook\_page\_top\(\)和hook\_page\_bottom\(\)调用。

4. Renderer（以前drupal\_render\(\)）在渲染'\#type' =&gt; 'html'数组上调用，它使用html.html.twig模板，返回值是一个HTML文档作为字符串。

5. 这些HTML字符串作为Response（特别是一个HtmlResponse对象，它是一个更专门的子类Response）返回。

**第1-2步产生&lt;body&gt;\(page.html.twig\)。第3-4步产生&lt;html&gt;\(html.html.twig\)。第5步发送一个包含&lt;html&gt;的响应对象Response。**

### 在有限的环境中渲染HTML

要在有限的环境中呈现HTML页面，例如在安装或更新Drupal时，或当您将其置于维护模式时，或者发生错误时，将使用更简单的HTML页面渲染器来渲染这些裸露页面：[`BareHtmlPageRenderer`](https://api.drupal.org/api/drupal/core!lib!Drupal!Core!Render!BareHtmlPageRenderer.php/class/BareHtmlPageRenderer/8)。

