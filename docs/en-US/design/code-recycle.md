# Code cycle: may be the syntax query that currently supports the most languages
- 400+Grammar Parses
- Like/selector two query modes
- Chain query; Multi level processing
- Automatically determine file language based on extension name

## Normal Query
- Search based on text; Query through regular expressions
- Although the above two query methods have strong universality in most cases, they are limited in some specific situations

For example, query the types of counts contained in Class A in the following code
```ts
class A{
    value:string
    count:number
}
```

## Grammar queries - code recycle
- You can directly use the like query mode `class A{ [[{]] count: [[$var]] [[}]] }`, which will directly match the type of the count and save it to the `var` variable for use
- Alternatively, using the selector mode `ClassDeclaration:has(>Identifier[value=A]) PropertyDeclaration:has(>[value=count])>NumberKeyword:infer(var)` will also be saved to the `var` variable

### Like query mode
- Like mode is similar to regular text in most cases, but it can ignore the impact of formatting. `let a=6` and `let a = 6` are parsed into a syntax tree in like mode, so there is no need to worry about the matching content being affected by formatting

### Selector query mode
- Use CSS selectors to select nodes and determine contextual queries
> The selector can internally call the like mode through `:like(xx)`

### Complete query context
- Not just for one query, `code recycle` currently allows for multiple different file queries at once. Each query result can be used as the scope of the next query, calling the already found results for adding/modifying/deleting
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

## How to use it?
- `code-recycle` currently supports both `cli` and `VSCode extension`
- You can refer to [quickstart-cli](https://wszgrcy.github.io/code-recycle/#/en-US/quickstart-cli)
- You can pull [demo repo](https://github.com/wszgrcy/code-recycle-plugin-script)to quick start

> git clone https://github.com/wszgrcy/code-recycle-plugin-script.git