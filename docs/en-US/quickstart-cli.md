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

## Config
- You can manually specify `CR_LANG=en` if the language display is incorrect

```
> npx code-recycle --help
Usage: code-recycle [options] <file-path>

Arguments:
  file-path             Script path

Options:
  --path [file-path]    Workspace path, relative path for use; the default value is the current directory.
  --root [file-path]    Root path; default is the same as path.
  --dryRun              dryRun mode (default: false)
  -c,--config [config]  Configuration file path; default is to look for 'code-recycle.json' in the current directory. (default: false)
  -h, --help            display help for command
```
- `--config`

?> "gitCloneTmpDir": Use git to pull the saved temporary directory; Default to system temporary directory

?> "treeSitterParserDir": tree-sitter build[wasm repo](./design/css-syntax-query?id=supported-languagesgrammar)

```jsonc
// code-recycle.json
{
  "treeSitterParserDir":"/path/to/tree-sitter-wasm-bundle"
}
```

## More?

- [Script Util](./script-util.md) Introduce