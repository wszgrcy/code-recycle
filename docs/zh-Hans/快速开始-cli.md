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

## 更多?

- [脚本工具](./脚本工具.md)介绍