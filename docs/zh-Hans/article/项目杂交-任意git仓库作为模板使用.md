# 项目杂交?Git仓库任意位置作为模板组合初始化
- 目前我们初始化项目,可能会使用Github中的`Use this template`,或者将某个仓库直接拉取
- 但是更多的是仓库中某个文件夹内存放的实例,开发者不会专门为模板单独建一个仓库,这时候我们就需要拉取整个仓库,然后提取出对应文件

## 可以使用`sparse`拉取
- 当然,Git也可以支持拉取部分文件夹,但是,这么繁琐的命令,你会每次都敲一遍吗?

```shell
git clone --filter=blob:none --no-checkout --sparse xxxx --depth 1 --branch yyyy ./zzz
cd ./zzz
git sparse-checkout set foo
git checkout yyyy
```

## `Code Recycle`中的Git仓库拉取

![](https://cdn.jsdelivr.net/gh/wszgrcy/code-recycle@1.1.2/docs/zh-Hans/image/git-template-demp.png)

- `Code Recycle` 目前是一个VSCode拓展,支持[Git仓库拉取](https://wszgrcy.github.io/code-recycle/#/zh-Hans/%E8%AE%BE%E8%AE%A1/%E8%87%AA%E5%AE%9A%E4%B9%89%E8%A7%84%E5%88%99?id=git%e6%a8%a1%e6%9d%bf)
- 可以在拉取任意位置的内容,写入到任意位置
- 可以一次性拉取多个仓库,放入到指定位置
> 你的初始化项目,不一定来自一个仓库
- 如果你觉得麻烦,可以直接修改上面的资源`git-template-demo`,资源已经放到在[公开区](https://wszgrcy.github.io/code-recycle/#/zh-Hans/%E5%85%AC%E5%BC%80?id=%e6%b7%bb%e5%8a%a0%e5%85%ac%e5%85%b1%e8%b5%84%e6%ba%90%e4%bd%bf%e7%94%a8).你可以直接复制后修改拉取链接即可使用
> 或者直接修改传入参数为[交互获取](https://wszgrcy.github.io/code-recycle/#/zh-Hans/%E8%AE%BE%E8%AE%A1/%E8%87%AA%E5%AE%9A%E4%B9%89%E8%A7%84%E5%88%99?id=%e5%8a%a8%e4%bd%9c-%e5%85%a8%e5%b1%80%e5%8f%98%e9%87%8f)或[视图化操作](https://wszgrcy.github.io/code-recycle/#/zh-Hans/%E8%AE%BE%E8%AE%A1/%E8%87%AA%E5%AE%9A%E4%B9%89%E8%A7%84%E5%88%99?id=%e8%a7%86%e5%9b%be%e5%8c%96%e5%8a%a8%e4%bd%9c),`Code Recycle`提供了丰富的代码修改操作,满足大部分场景使用

### 快速开始
- 如果你已经在考虑中,不妨可以[看一下文档](https://wszgrcy.github.io/code-recycle/#/zh-Hans/README)如何使用

