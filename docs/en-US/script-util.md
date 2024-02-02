Script tools abstract the most commonly used script query/replacement and template copying functions, making it convenient for users to quickly get started
---
## Basic operations
- Using the following file as an example

```ts
let a = 6;
let b= '123';
```

### Read context nodes
```ts
  {
    query: `VariableDeclarationList:has(Identifier[value=a]) LetKeyword`,
    replace: util.statement`${''}1`
  }
```

- When not using `util.statement`, it is treated as a regular string. When using `util.statement`, it is a tagged template that can use some contextual parameters to read relevant content and return a string
- The node content reading method is`xx.yy.zz`, and if it is empty string, it defaults to the current node
- Both `query` and `replace` attributes can use `statement`
- Result:`let`replace`let1`

```diff
- let a = 6;
+ let1 a = 6;
  let b= '123';
```

### Read parent content
```ts
{
  query: `VariableDeclarationList:has(Identifier[value=a])`,
  children: [{
      query: `LetKeyword`, replace: util.statement`${'parent'}1`
  }],
}
```
```diff
- let a = 6;
+ let a = 61 a = 6;
  let b= '123';
```

### Query multiple nodes
```ts
{
  query: `LetKeyword`,
  multi: true,
  replace: `const`
}
```
```diff
- let a = 6;
+ const a = 6;
- let b= '123';
+ const b= '123';
```

### Named variable
```ts
{
  query: `VariableDeclarationList`,
  children:[
    {query:`LetKeyword`,name:'letVar'}
  ],
  replace:util.statement`${'letVar'}1`
}
```

```diff
- let a = 6;
+ let1
  let b= '123';
```

### Delete Node
```ts
{
    query: `LetKeyword`,
    multi: true,
    delete:true
}
```
```diff
- let a = 6;
+  a = 6;
- let b= '123';
+  b= '123';
```

### Insert before/after node
```ts
{
    query: `LetKeyword`,
    multi: true,
    insertBefore:true,
    // insertAfter:true,
    replace:`/**comment*/`
}
```
```diff
- let a = 6;
+ /**comment*/let a = 6;
- let b= '123';
+ /**comment*/let b= '123';
```

### optional
- When querying normally, if no results are found, an exception error will be thrown. Therefore, if it is uncertain whether there is an `optional` available, after the query fails, there will be no exceptions or callbacks, and the child query will not continue to be executed


> Can set `description:'' `to output error messages

```ts
{
    query: `AAAA`,
    optional: true,
    children: [
        { query: `BBBB` }
    ]
}
```

### callback/listCallback
- If the regular query cannot meet the requirements, a callback customization can be used, and the nodes returned by the callback will also be added to the modification list
- When`multi: true` enable `listCallback`

```ts
{
    query: `LetKeyword`,
    multi: true,
    callback: (context) => { return util.setChange.contextNode(context,'')},
    listCallback: (list, self) => { }
}
```
```diff
- let a = 6;
+  a = 6;
- let b= '123';
+  b= '123';
```

## Advanced Operations

### Multi file operation layer
- Different file operation layers can perform different processing (here is a file demonstration)
- Can use `data` to pass the data he has processed

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
                }
            ]
        }, {
            path: './def1.ts', list: [
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
```diff
- let a = 6;
+ let let = 6;
  let b= '123';
```

### Context mapping modification
- By default, the context is obtained from the parent (the top valid context is determined based on the file/input content)
- You can also change the parent query node

```ts
{
    path: './def1.ts', list: [
        {
            query: `VariableDeclarationList`,
        },
        {
            query: `NumericLiteral`,
            children: [
                { parentMap: 'parent2.0', query: `Identifier`, replace: `changed` }
            ]
        },
    ]
}
```
- Under normal circumstances, there is no node after the `NumericLiteral` node, but the content can be queried by changing the parent node

```diff
- let a = 6;
+ let changed = 6;
  let b= '123';
```


## More
- The document is constantly improving, and some features may not be displayed. If you encounter any related issues, you can ask questions at [Issues](https://github.com/wszgrcy/code-recycle/issues)