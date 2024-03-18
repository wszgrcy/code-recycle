## Initializing a Project with Any Git Repository - `Code Recycle`
- For the sake of development, it is generally used to initialize the project on the template repository in Git.
- When wanting to know about the features of a certain project, it might be run an instance under a repository for the project.
- Or, in some folders within the repository, there are various file templates that provide initialization for some modules.
- For the three above scenarios, we all need to pull the repository, but sometimes we only need to pull a portion of the repository, in which case it is not necessary to manually pull the repository. It is recommended to use `Code Recycle` and perform custom pulling through a few lines of configuration.

## git clone full

```yml
changeList:
  - type: copy
    from: https://github.com/maximegris/angular-electron.git
    to: ./ae
    source: git
```

## git clone part
```yml
changeList:
  - type: copy
    from: 
      url: https://github.com/microsoft/vscode-extension-samples.git
      match:
        - /l10n-sample
      output: /l10n-sample
    to: ./l10n
    source: git
```

## git clone as template
```js
module.exports = async (util, rule, host, injector) => {
  let list = await util.changeList([
    {
      type: 'copy',
      source: 'git',
      from: {
        url: 'https://github.com/angular/angular-cli.git',
        match: '/packages/schematics/angular/directive/files',
        output: '/packages/schematics/angular/directive/files',
      },
      pathTemplate: '@angular-devkit',
      contentTemplate: '@angular-devkit',
      pathTemplateSuffix: '.template',
      templateContext: { name: 'hello', standalone: true, selector: 'hello', 'if-flat': (input) => '' },
      to: './hello-directive'
    },
  ]);
  await util.updateChangeList(list);
};
```

## More?
- The tool currently supports the execution of `CLI` and `VSCode Extension`. Script Support `yaml`/`js`/`ts`
- You can view [document](https://wszgrcy.github.io/code-recycle/#/en-US/README) learn more
- If you want to see more instances, you can [visit the repository](https://github.com/wszgrcy/code-recycle-plugin-script) view and Run
- If you are already interested, you can [start quickly](https://wszgrcy.github.io/code-recycle/#/en-US/quickstart)