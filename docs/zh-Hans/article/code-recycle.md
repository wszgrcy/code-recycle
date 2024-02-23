# code-recycle: 可能是目前支持语言最多的语法查询
- 400+种的语法解析
- like/selector两种查询模式
- 链式查询;多层级处理
- 根据拓展名自动确定文件语言

## 普通查询
- 根据文本进行查询;通过正则表达式查询
- 虽然上面两种查询方式在大多数情况下通用性非常强,但是在一些特定情况下就捉襟见肘了

比如,查询下面代码中 A 类包含的 count 的类型
```ts
class A{
    value:string
    count:number
}
```
## 语法查询 - code recycle
- 你可以直接使用 like 查询模式 `class A{ [[{]] count: [[$var]] [[}]] }`,将会直接匹配到 count 的类型并保存到`var`变量中供使用
- 或者使用 selector 模式 `ClassDeclaration:has(>Identifier[value=A]) PropertyDeclaration:has(>[value=count])>NumberKeyword:infer(var)` 同样会保存到`var`变量中

### like查询模式
- like 模式在大多数情况下都与普通文本一样,只不过可以无视格式化带来的影响,`let a=6`与`let a = 6`在like模式下会被解析为一种语法树,所以不用担心匹配的内容会被格式影响

### selector 查询模式
- 使用 css选择器选择节点,确定上下文关系查询
> selector内部可以通过`:like(xx)`调用like模式

### 完整的查询上下文
- 不止是进行一次查询,`code recycle`目前可以一次进行多种不同文件查询,每一次查询结果可以作为下一次查询的范围,调用已经查询到的结果,进行 新增/修改/删除

```ts
[
        {
            name: 'file1',
            path: './def1.ts', list: [
                {
                    query: `LetKeyword`,
                    callback: (context) => {
                        context.data = context.getNodeValue()
                    },
                },
                {
                    query: `let a=[[$var]]`,
                    replace:{var:'7'},mode:'like'
              
                }
            ]
        }, {
            path: './def2.ts', list: [
                {
                    query: `Identifier`,
                    callback: async (context) => {
                        return util.setChange.contextNode(context, context.getContext('root.file1.0').data)
                    },
                }
            ]
        }
]
```

## 如何使用?
- `code-recycle`目前同时支持`cli`与`VSCode extension`
- 你可以参考[快速开始-cli](https://wszgrcy.github.io/code-recycle/#/zh-Hans/%E5%BF%AB%E9%80%9F%E5%BC%80%E5%A7%8B-cli)