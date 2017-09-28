# 命名和放置模块

我们使用“**hello”**作为模块的名字,来做示例演示

### 模块命名规则

1. 必须以字母开头

2. 只能包含小写字母与下划线。

3. 必须唯一，不能与模块、主题、或配置文件重命。

4. 不能使用保留字:src、lib、vendor、assets、css、files、images、js、misc、templates、includes、fixtures、Drupal

**重要提示：**确保不要在模块的机器名称中使用大写字母，因为Drupal将无法识别您的钩子实现。请参阅了解Drupal模块的挂钩系统。

### 放置模块（未你的模块创建一个文件夹）

我们使用"**hello\_world**"作为模块机器名

鉴于我们选择的机器名称是“hello\_world”，请通过在Drupal安装中的路径：将模块放置到文件夹中，

但通常最好为自己的模块设置一个专用的位置

**/modules/custom/hello\_world    
**

**/sites/all/modules/hello\_world    
**

**/modules/hello\_world    
**

这里在drupal8安装目录下创建**/modules/custom/hello\_world    
**目录\(见下图\)。

![](/assets/1.png)

