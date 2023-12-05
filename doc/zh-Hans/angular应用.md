# Angular使用动态代码片段进行快速开发
- 目前,对于 Angular 中的 指令/管道/组件的相关使用,通常,我们需要先引入(ts import && ng imports),然后再调用;如果是第一次使用,我们还需要创建
- 这种开发模式往往会打断我们的开发思路,因为我们需要创建=>引入=>使用,不停的切换文件,转换思路
- 那么如何改变这种写法,让代码的实现变得与依赖注入一样简单?只考虑使用,不考虑其他问题?
- 这个方案,我称之为**代码级依赖注入**,而实现的手段,我称之为**动态代码片段**

## 使用 Code Recycle 实现动态代码片段
- 一般的代码片段: 调用时的插入内容已经确定,且只能插入到当前文件
- 动态代码片段: 插入时会捕获相关上下文,调用一个**动作**通过**动作**处理其他文件,实现**依赖注入**
## Code Recycle 提供了部分开箱即用的 Angular 功能
- `Code Recycle`拥有一个**可视化可编程的设计器**, 可以进行各种`有确定逻辑`的代码生成设计.
> 你可以理解为,它有一个可以自定义的原理图
- 目前也提供了一些**动作**和**动态代码片段**,方便 Angular 开发者来使用
> 所有处于**公共区**的内容都可以直接调用或根据自己的使用习惯进行**修改**
### **动态代码片段** html中 指令/管道 自动引用
- 该动作自动查找指定区域的管道和指令,如果存在则会在调用时进行引用,不存在则会在指定文件夹中创建一个空的实现,然后进行引用

### **动态代码片段** reference 
- 执行时自动在ts文件中插入 `@ViewChild {{name}}:any` 及导入(如果不存在)

### **动态代码片段** html中 方法/属性 自动生成
- 执行时会自动在ts文件中插入 方法/属性 

### **动态代码片段** material design
- 执行时会插入相关引用(如果不存在),并且生成相关ts代码(如果有)

#### column
- 调用此片段时会自动向`{{columnList}}`中插入名字
### **动作** 组件模板
- 执行时会自动创建组件及最近模块(Model||Standalone Component)插入相关引入
> 类似官方的原理图
---
## 其他
## 那么在哪里可以找得到呢?
- 目前支持`Vscode`与所有系统,目前已经在[微软插件市场](https://marketplace.visualstudio.com/items?itemName=LDXCODE.code-recycle)上架  
## 其他语言/框架如何使用?
- 任何语言/框架都可以使用,但是目前只有 Angular 提供了一些开箱即用的功能
> 即开发者用**设计器**实现了上述的内容并`公开`到**公共区**
- 其他语言/框架可以参考公共区已有的一些**动作**/**代码片段**实现自己所需要的生成

## 相关资源
- [视频](https://www.bilibili.com/video/BV1wc411i7pZ/) Angular中使用动态代码片段快速开发
- [https://www.bilibili.com/video/BV1Nb4y1u7FP/](https://www.bilibili.com/video/BV1Nb4y1u7FP/) 介绍插件的视频
- [https://www.bilibili.com/video/BV1Vj411J7VZ/](https://www.bilibili.com/video/BV1Vj411J7VZ/) 插件的一些使用演示
- [插件中文说明](https://github.com/wszgrcy/code-recycle/blob/main/doc/README.zh-Hans.md)
- [https://github.com/wszgrcy/code-recycle](https://github.com/wszgrcy/code-recycle) 目前保存i18n的仓库,也是未来开源的仓库
- [教程合集](https://space.bilibili.com/31978940/channel/collectiondetail?sid=1891886)