# Script development
```ts
import type { ScriptFunction } from '@code-recycle/cli';
const fn: ScriptFunction = async (
    // 提供快速开发的一些方法
    util, 
    // 一些独立的规则,供单独调用
    rule, 
    // vfs 与 fs 类似,允许清空未写入内容,glob查询等功能
    host, 
    // 依赖注入
    injector) => {
};
export default fn;
```

- [Function definition](api-docs/interfaces/ScriptFunction.html ':ignore')
- After the function is executed, it will write the contents modified in the VFS to the file system.


---

## util
- Enclose common functions for quick search and query.

```ts
// 查询文件的配置
let list = await util.changeList([]);
// 将修改更新到VFS中
await util.updateChangeList(list);
```

```yaml
changeList:
```

### FileQueryLayer
- [Document](api-docs/interfaces/FileQueryLayer.html ':ignore')
- Allow specifying paths/using glob to input text for parsing.

> When no parser is specified, determine the parser to use based on the file extension.

### NodeQueryItem
- [Document](api-docs/types/NodeQueryItem.html ':ignore')
- In the query layer, the `list` is passed the query node configuration for querying.

#### Query pattern
- [like](/en-US/mode/like): Similar to traditional search, but based on AST/CST search, no intelligence.
- [selector](/en-US/mode/selector): A general implementation of `css selector`, using `css selector` to query any language, supporting internal `like` query pattern, and low intelligence.

#### Context
- The first-level node list passed in the `list` , with the entire file as the query range, and the `children` will continue to query based on the parent query results.
- The context will be passed in some callback functions.

```ts
{
parentMap: (context) => {},
callback: (context, index) => {},
}
```

- When using functions in `AutoDATA` type properties, it will be passed in.

```ts
{
query: (context) => {},
replace:(context) => {}
}
```


##### Read context
- [FileQueryLayer](api-docs/interfaces/FileQueryLayer.html ':ignore') and [NodeQueryItem](api-docs/types/NodeQueryItem.html ':ignore') both can be specified with a name `name:'xx'` for context reading.
- Through `context.getContext`, you can read the context of any node, and it takes a path as an argument.

> `root.xx`It represents the context of the `name:'xx'` query layer in the entire context.
> `item.xx`It represents the context of a query result in the current query layer.  
> `parent1`/`parent2`/`parent...`Read the context of the parent node of any layer.
> `parent.1`Read the first context result of the parent node.  
> `parent.xx`Read the descendants of the parent node with the name `xx` (not the children).  
- When `multi` is `true`, access the context of the child node's parent node's `childrenIndex.queryIndex`/`childrenName.queryIndex`.

```ts
{
query: `SourceFile`,
children: [
    //childrenIndex 0
    {   //childrenName var1
        name: 'var1', 
        query: 'VariableStatement', multi: true }
    ],
callback(context, index) {
  // let result = context.getContext('0.0');
  let result = context.getContext('var1.0');
},
}
```


#### Query result
- By default, every query must have a result, otherwise an exception will be thrown.
- Use `optional` to indicate that this query may not have a result (it will not throw an exception, but all child queries will be terminated).
- Use `nullable` to indicate that this query may not have a result, but the child queries will be executed normally. It needs to be combined with `parentMap`.
- By default, it returns only one query result, and you can use `multi` to return a list of query results.

> If the query result is an empty array, it is also considered to have no query results.
- Use `allOf` to indicate that all queries in the array must succeed, and `optional` to force it to be `false`.
- Use `oneOf` to indicate that only one query in the array can succeed, and `optional` to force it to be `true`.
- Use the `anyOf` field to indicate that all queries within the array have a successful query, and then stop querying other fields. Use `optional` to force it to `true`.
- Use the `not` query to change the result from failure to success. Use `optional` to force it to `true`.

#### query
- Support multiple formats for input at the same time.
- String - Interpolation Pipeline

> Without using `{{}}`, it is completely consistent with regular strings; if you want to input `{{xx}}` string, you can use escape `\\{{xx}}`.

```ts
{query:`let{{'parent'|ctxValue}}`}
```

> `let{{'parent'|ctxValue}}` indicates using the `ctxValue` parameter for the `parent` field, supporting multiple pipelines and parameter usage.  

> Support pipelines:  
> `ctxValue` Read the value of the context node.  
> `ctxInferValue`Read the variable saved during the query process.  
> `ctxData`Read the additional data added to the node.  
> `path.xxx`(join,normalize,resolve,relative,basename,dirname,isAbsolute,getSystemPath,split) [Reference](api-docs/classes/Util.html#path ':ignore');Path processing  
> `lodash.xxx`/`_.xxx` [Reference](https://lodash.com/docs)  

- Custom pipeline`util.setCustomPipe`
- Returned through the function

> Can be manually called using `context.pipe`.

```ts
{
query:(context)=>{return 'let'},
}
```

### replace
- The parameters in the `query` part are the same, and when an object is passed in, it indicates replacing the variables in the query with the corresponding ones.

> The way to get the variable in the like query is`[[$var]]`  
> The way to get the variable in the selector is`:infer(var)`

---
### FileCopyLayer
- [Document](api-docs/types/FileCopyLayer.html ':ignore')
- Copy files from the local/git repository to a specified location.
- The file can be a template, and it will be automatically rendered when it is passed into the context.
- `ignoreList` is the file to be ignored, such as `.gitignore`, and `excludeList` excludes certain files.

> In the current design, the files to be ignored are first traversed and then ignored. Therefore, if there are performance issues, you can use `excludeList` to exclude the specified folder first.  
> The files to be ignored themselves will not be ignored, and they need to be added manually to the configuration.
#### Template
- Support multiple  templates,  `@angular-devkit`(path)/`handlebars` template engine supports partial variable awareness, and if the context does not provide it, it will prompt for interaction.
- Path template only has `@angular-devkit`, and `__name@toUpper__` is a kind of pipeline writing style, equivalent to `toUpper(name)`.
- Using `pathTemplateSuffix` can remove the template suffix.

### FileCreateLayer
- Create a new file.

---


## rule
- [Document](api-docs/classes/Util.html#rule ':ignore')

## host(VFS)
- [Document](api-docs/classes/ReadScopedHost.html ':ignore')
- In VFS, all paths are in posix format.

## Examples
- [Link](https://github.com/wszgrcy/code-recycle-plugin-script/tree/master/examples)