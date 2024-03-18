## Code completion
- Create `snippet` in the `script. dir` folder and enter it
- Write completion code configuration in `manifest.json/yml`
- [examples](https://github.com/wszgrcy/code-recycle-plugin-script/tree/master/snippet)
## `manifest` Config
```ts
interface SnippetSaveData {
  enable?: boolean;
  prefix: string[];
  body: string;
  languageList?: string[];
  name?: string;
  pattern?: string;
  description?: string;
  script?: string
  parameters?: Record<string, any>;
  regexp?: {
    pattern: string;
    flag: string;
  };
}
```

## Related calls
- [Document](api-docs/classes/Util.html#rule ':ignore')
- Use `rule. editorInput` to read relevant configurations
- Manually trigger the insertion of code snippets using `insertSnippet`
> You can set `body` to ` `(blank string placeholder) to call

