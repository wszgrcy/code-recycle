# 如何在 VSCode 中自定义搜索逻辑?
- 搜索/替换,在每个编辑器都存在的功能
- 主要用来进行文本的替换
- 但是在代码开发中,有时候搜索结果过多,想要筛选出合适的内容就不是那么容易
- 我们往往需要在某个`块`中或某个特定逻辑的位置(例如xx函数内第y个参数名)进行搜索/替换
- 这时候就需要自定义我们自己的搜索逻辑,来满足需求
## Code Recycle 中提供的自定义视图动作
- `Code Recycle`目前是vscode中的一个拓展,可以通过指定语法的解析器,进行查询内容,并且进行相关操作.
- 目前已经支持了视图显示,并且可以自定义视图,满足用户的各种内容
- 目前开箱即用的提供了一个自定义搜索逻辑`动作`,当然您也可以直接复制此`动作`,修改为自己想要的

![custom-interactive](https://cdn.jsdelivr.net/gh/wszgrcy/code-recycle@1.0.8/doc/image/custom-interactive.jpg)
![demo](https://cdn.jsdelivr.net/gh/wszgrcy/code-recycle@1.0.9/doc/image/view-action/demo.webp)

### 除了自定义搜索 Code Recycle 还可以做什么
- 最初,拓展设计为了更方便的定位文件内容,**处理代码级可重复逻辑**,修改文件内容
- 所以只要想处理的内容**存在逻辑**,都可以使用本拓展实现,只不过最近支持了自定义视图,方便大家更容易使用

## 其他
## 那么在哪里可以找得到呢?
- `目前`支持`VSCode`与所有系统,目前已经在[微软插件市场](https://marketplace.visualstudio.com/items?itemName=LDXCODE.code-recycle)上架 

- 安装登录之后,打开命令面板输入`code-recycle`,进入配置;进入公共区 搜索`interactive`找到公开的视图动作并添加;在侧边栏找到`Code Recyle`视图,打开选择刚才添加的动作

![add-custom-interactive](https://cdn.jsdelivr.net/gh/wszgrcy/code-recycle@1.0.9/doc/image/add-custom-interactive.jpg)

## 相关资源
- [视频:vscode中自定义搜索逻辑](https://www.bilibili.com/video/BV1ec411y7JH/) 
- [视频:初始化项目-模板生成可撤销](https://www.bilibili.com/video/BV1pj411L7yQ/) 
- [视频:图灵完备验证](https://www.bilibili.com/video/BV19w411b7qx/) 
- [视频:Angular中使用动态代码片段快速开发](https://www.bilibili.com/video/BV1wc411i7pZ/) 
- [视频:介绍插件](https://www.bilibili.com/video/BV1Nb4y1u7FP/) 
- [视频:插件的一些使用演示](https://www.bilibili.com/video/BV1Vj411J7VZ/) 
- [插件中文说明](https://github.com/wszgrcy/code-recycle/blob/main/doc/README.zh-Hans.md)
- [https://github.com/wszgrcy/code-recycle](https://github.com/wszgrcy/code-recycle) 目前保存i18n的仓库,也是未来开源的仓库
- [教程合集](https://space.bilibili.com/31978940/channel/collectiondetail?sid=1891886)