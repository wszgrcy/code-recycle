## Code Recycle
> 可编程的高级语法查询/替换工具

## 概述

用于快速初始化项目;代码重构;动态代码片段;
减少开发中的重复性逻辑

> **什么是重复性逻辑?**  
> 如果某些操作不需要进行考虑,只需要按照一定规则进行处理,那么就可以视为`重复性逻辑`

---

## 特性
### 模板
- 快速裁剪与自由组合
- 冲突的交互处理
- 生成后可以撤销
- [拉取Git仓库指定文件作为模板](/zh-Hans/脚本规则?id=osgitclone)

### 代码片段
- 动态代码片段,跨文件生成内容

### 自定义规则
- 语言无关,框架无关,只要支持语法解析即可
- [CSS语法查询,支持400+种的语法解析](/zh-Hans/设计/css语法查询?id=说明)
- [抽象语法树的语法查询调试](/zh-Hans/设计/css语法查询?id=语法查询)
- 视图化操作

---

## 支持
|VSCode|CLI|
|-|-|

## 支持操作系统
| Windows  | Linux | OSX |
| ------- | ------- | ---- |

## 使用方式
- [VSCode脚本](./快速开始-脚本.md)
- [命令行CLI](./快速开始-cli.md)

?> VSCode/CLI调用的脚本格式相同;VSCode额外支持代码片段脚本和视图脚本运行在特定环境;CLI目前允许使用`ts`脚本

## 快速体验

### VSCode脚本
- `git clone https://github.com/wszgrcy/code-recycle-plugin-script.git`
- 修改编辑器设置`settings.json`

```json
"code-recycle.script": {
    "dir": "/path/to/code-recycle-plugin-script"
}
```



## 关于开源

- 当开发者能从此插件中产生盈利并能维持自身生活需要时,会进行开源
- 目前本插件没有任何盈利行为
- 如果你有什么比较好的商业化想法,也可以联系我`wszgrcy@gmail.com`