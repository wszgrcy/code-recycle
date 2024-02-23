## 安装
- `npm i @code-recycle/cli -D`

## 创建
```ts
// test/test.ts
/**
 * let a = 6;
 */
// index.ts
import type { ScriptFunction } from '@code-recycle/cli';
let fn: ScriptFunction = async (util, rule, host, injector) => {
  let list = await util.changeList([{ path: './test/test.ts', list: [{ query: 'let a=[[$var]]', mode: 'like', replace: { var: '7' } }] }]);

  await util.updateChangeList(list);
};
export default fn;

```

## 执行
- 命令行 `npx code-recycle ./index.ts`
> `package.json`脚本`start: "code-recycle ./index.ts"` 执行`npm start`
- `./test/test.ts` 将会修改 `6` => `7`


## 配置
```
> npx code-recycle --help
Usage: code-recycle [options] <file-path>

Arguments:
  file-path             脚本路径

Options:
  --path [file-path]    工作路径,用于使用时的相对路径;默认为当前文件夹
  --root [file-path]    根路径;默认与 path 相同
  --dryRun              演练模式 (default: false)
  -c,--config [config]  配置文件路径;默认会查找当前文件夹下的'code-recycle.json' (default: false)
  -h, --help            display help for command
```
- `--config`

?> "gitCloneTmpDir": 使用git拉取保存的临时目录;默认为系统临时目录

?> "treeSitterParserDir": tree-sitter构建的[wasm仓库](./设计/css语法查询?id=支持语言语法)

```jsonc
// code-recycle.json
{
  "treeSitterParserDir":"/path/to/tree-sitter-wasm-bundle"
}
```

## 更多?

- [脚本工具](./脚本工具.md)介绍