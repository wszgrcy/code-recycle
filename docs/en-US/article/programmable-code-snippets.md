## Implementing programmable code snippets in VSCode - `Code Recycle`
- How to customize code snippets in the editor? Provide the completion prefix, provide the completion content, and then you can use it directly
- But specific content can only be inserted in the current file and input location, sometimes it may not meet the requirements
- If we want to introduce a service that automatically creates when it does not exist, we can only rely on ourselves because the code snippet is `static` and cannot be `programmed`
- If you have such a need and want to implement it, why not give it a try with `Code Recycle`

## Import a service
- Create code snippet configuration

```json
{
    "prefix": [
        "import"
    ],
    "body": " ",
    "regexp": {
        "pattern": "\\.([\\p{L}\\p{N}]+)",
        "flag": "u"
    },
    "pattern": "**/*.ts",
    "dynamicMode": true,
    "script": "./import-class.ts"
}
```
- Implement call function

```ts
let fn: ScriptFunction = async (util, rule, host, injector) => {
  let importName = util.documentContext.snippetParameters![1];
  let _ = util.lodash;
  let className = _.upperFirst(_.camelCase(importName));
  let rootCtx = util.initContext();
  await util.changeList(
    [
    // Check if the class exists
      {
        path: `*.ts`,
        name: 'classPath',
        glob: true,
        list: [
          {
            query: `export class ${className}`,
            mode: 'like',
            optional: true,
            callback(context, index) {
              let classPathCtx = context.getContext('root.classPath');
              classPathCtx.data = context.node!.path!;
            },
          },
        ],
      },
    ],
    rootCtx
  );
  let filePath = rootCtx.getContext('root.classPath').data;
  if (!filePath) {
    // Create from template
    await util.changeList([
      {
        type: 'copy',
        from: join(__dirname, './template/__name@dasherize__.ts'),
        to: './',
        pathTemplate: '@angular-devkit',
        contentTemplate: '@angular-devkit',
        templateContext: { name: importName },
      },
    ]);
    let changedRecord = host.records();
    filePath = util.path.normalize((changedRecord[0] as any).path);
  }
  let pathRelative = require('../shared/path-relative');
  // insert reference
  let changed = await util.changeList([
    {
      path: util.filePathGroup.currentPath,
      list: [
        {
          range: [0, 0],
          replace: `import {${className}} from '${pathRelative(util.filePathGroup.currentPath, filePath, util)}'\n`,
        },
        {
          range: util.documentContext.insertRange![0].range,
          replace: `let ${importName} = new ${className}()`,
        },
      ],
    },
  ]);

  await util.updateChangeList(changed);
};
```
- When entering `import.hello` in the `ts` file in the editor, and completing the completion, the `Hello` class will be automatically introduced and initialized

## More?
- [examples](https://github.com/wszgrcy/code-recycle-plugin-script/tree/master/snippet)
- The tool currently supports the execution of `CLI` and `VSCode Extension`. Script Support `yaml`/`js`/`ts`
- You can view [document](https://wszgrcy.github.io/code-recycle/#/en-US/README) learn more
- If you want to see more instances, you can [visit the repository](https://github.com/wszgrcy/code-recycle-plugin-script) view and Run
- If you are already interested, you can [start quickly](https://wszgrcy.github.io/code-recycle/#/en-US/quickstart)