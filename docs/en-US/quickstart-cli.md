## Install
- `npm i @code-recycle/cli -D`

## Create
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

## Exec
- command `npx code-recycle ./index.ts`
> `package.json`script`start: "code-recycle ./index.ts"` command `npm start`
- `./test/test.ts` will change `6` => `7`

## More?

- [Script Util](./script-util.md) Introduce