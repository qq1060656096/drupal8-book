# 6.2 可冒泡的元数据

#### 缓存元数据

缓存上下文:是指可能会影响渲染的上下文，如用户角色和语言等，当没有指定缓存上下文时，这表明渲染数组不会因为任何上下文而有所不同。

缓存tags:渲染依赖的数据，如节点或用户账户等。当这些实体内容改变时，能使我们的缓存内容自动失效。如果数据由实体组成，你能使用\Drupal\Core\Entity\EntityInterface::getCacheTags\(\)成生适当的tags；配置对象也有类似的方法。

缓存max-age:渲染数组缓存的最大过期时间。默认是持久缓存即\Drupal\Core\Cache\Cache::PERMANENT。

冒泡的元数据:缓存元数据 + \#attached + \#post\_render\_cache回调。\#attached键用于指定附件，这里的附件是指附加的资源，包括CSS、JS和HTML标签等。

默认的渲染缓存上下文:每一个渲染数组使用\#theme来指定要使用的主题模板，几乎每个渲染数组都包含字符串翻译\(即将文本放在t\(\)函数内\)。这就是为什么Drupal添加了对缓存上下文\(‘theme’和’languages:’.LanguageInterface::TYPE\_INTERFACE\)的响应。默认的缓存上下文是在required\_cache\_contexts键中的指定的。注意，对于一些高级用法，站点可以选择覆写这些默认的上下文需求。

在渲染元素时要考虑很多因素，比如缓存是否命中，命中又怎么做，没命中又怎么做。另外渲染数组是嵌套的，因此渲染是递归进行的，就像爬树一样自上而下，这里就涉及到元素的冒泡过程，即从孩子元素冒泡到它的父元素。具体的渲染过程很复杂，有兴趣的可阅读RenderInterface接口的相关文档。



