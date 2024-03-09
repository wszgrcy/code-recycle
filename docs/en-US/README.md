## Code Recycle
> A search/replace tool specifically designed for code programming
> Use more readable text to search for similar structures in the code

## Using scenario

- Search/replace
- Refactoring
- Initializing the project
- Dynamic code snippets



---

## Features
### Language Query
- Multi-language parsing; support for over 400 different grammatical parsing options.

- A way similar to normal queries, but more in line with the expectations of searchers.

> Normal queries only match the same text and do not consider the grammatical relationship between them. `like queries` provide results that are in line with the grammar of the programming language associated with the file.

```ts
let a    =     1;let b=`let a=1`
```
?> Using the query `let a=1`, normal queries can only find the content of the string, but in the `like query`, it will query the declaration in front of it.  
So you don't have to worry about the impact of different formatting on the queries, and you don't have to worry about the results of non-grammarical nodes.

- Multi-level queries; support different languages and different parsing results; quickly access results that have already been queried.
- Using VSCode extension can display AST for search and debugging
- Auto-determine parser based on suffix name.

### Template
- Multi-template engine
- Support automatic variable parsing and hint input.

> Currently, only a part of the variable parsing is supported.

- Request git repository on demand.
- Support template rollback.

### Structured Query Search
- The subsequent levels can use the contextual data from the previous ones
- The query results of the parent level limit the query scope of the child level

### Virtual file system
- All modified content will only be written into the file system after it is fully executed successfully.
- Support dryRun.

### VSCODE
- Dynamic code snippets; allow calling scripts to modify other files during code completion.
- Custom views; allow customizing an interactive search/replace tool.
- Support manual handling of template conflicts.
- Syntax query debugging for abstract syntax tree.

---

## Support
|VSCode|CLI|
|-|-|


| Windows  | Linux | OSX |
| ------- | ------- | ---- |

## [Quick start](./quickstart.md)

?> The script format for VSCode/CLI is the same; VSCode also supports running snippet scripts and view scripts in specific environments.






## About Open Source

- When developers can make a living from the plugin and maintain their lives, they will open source it
- Currently, this plugin has no profit-making behavior
- If you have any better commercial ideas, you can contact me at `wszgrcy@gmail.com`