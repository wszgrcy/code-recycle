## Code Recycle
> Programmable advanced syntax query/replacement tool


## Overview

Quickly initializes projects,Code refinement,Dynamic code snippets,Reduces redundant logic in development

> **What is redundant logic?**  
> If certain operations do not require consideration and can only be processed according to a certain rule, they can be considered as `repetitive logic`

---

## Features
### Template
- Quickly cut and freely arrange
- Conflict interaction handling
- Generated content can be cancelled.
- [Pull specific files from Git repository as template](/en-US/script-rule?id=osgitclone)

### Code snippets
- Dynamic code snippets, generate content across files

### Custom Rules
- Language-independent, framework-independent, as long as syntax parsing is supported.
- [CSS syntax query, supports over 400+ syntax parsing](/en-US/design/css-syntax-query?id=css-selector-support)
- [Syntax query debugging for abstract syntax trees](/en-US/design/css-syntax-query?id=syntax-query)
- Visual operation

---

## Editors Supported
|VSCode|CLI|
|-|-|

## Operating Systems Supported
| Windows | Linux | OSX |
| ------- | ------- | ---- |

## Usage
- [VSCode Script](./quickstart-script.md)
- [CLI](./quickstart-cli.md)

## Quick Experience

### VSCode Script(Recommend)
- `git clone https://github.com/wszgrcy/code-recycle-plugin-script.git`
- change editor `settings.json`

```json
"code-recycle.script": {
    "dir": "/path/to/code-recycle-plugin-script"
}
```



## About Open Source

- When developers can make a living from the plugin and maintain their lives, they will open source it
- Currently, this plugin has no profit-making behavior
- If you have any better commercial ideas, you can contact me at `wszgrcy@gmail.com`