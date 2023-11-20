# Code Recycle: Code Generator Designer

- How to develop quickly? The less code you write, the faster the development process.

- Then how do you write less? It's naturally to write the best implementations.

- But many times, in addition to the necessary logic, some peripheral code also needs to be implemented: declarations, registrations, references...... They are very similar in each use, but there is a bit of difference. This difference makes us repeatedly write the same code. Moreover, when implementing logic-related code, the change in thinking can also affect the development process.

- When doing code refactoring/upgrading/migration, there is also this situation. The main logic remains basically unchanged, but only some frameworks/calls are related to logic and the architecture-related code changes. For small projects, migration is done manually; but for large projects, it is very likely that some files will be missed or wrong in the repetitive mechanical labor, and every file needs to be checked before submission. In addition to wasting time, energy is also wasted; if a new function is inserted in the middle, and it is found that other functions have not been changed after the refactoring, it feels like it is directly cracked...

- So is there a way to customize this implementation?

- Yes! From now on, we will start to sell ourselves, starting with me...

## Introduction

![插件图](https://cdn.jsdelivr.net/gh/wszgrcy/code-recycle@1.0.1/doc/zh-Hans/image/插件图.jpg)

- It's not a library now, nor will it be open-sourced (for now), but it's supported in all systems, and it's already on the [Visual Studio Code Marketplace](https://marketplace.visualstudio.com/items?itemName=LDXCODE.code-recycle).
- The extension supports trimming files open in a project, quickly generating file templates; and provides a combination of `action` calling.
- The inspiration for implementing custom rules comes from Angular's [schematics](https://angular.io/guide/schematics), allowing users to set their own generation logic and call it through the UI.
- During the execution of `code snippets`, the parameters matching the extension can also be passed to `action` calls.
- If you're still unclear, let's say the most straightforward way: **If you can see some relationships between code with your naked eye and can manually implement modifications/ additions/ deletions, then this extension can solidify this logic and repeatedly implement it.**
  > Is it an AI model? No, all designs need to be implemented by themselves, but the implementation is just concretized.
  > Is it the mouse/keyboard recording? No, the repeated implementation of the `logic` is through the parser in the corresponding language, which determines the position for modification based on the grammar analysis. It is like the `feature point` positioning in the cheat code. The selector remains the same, and the generated code remains the same.
  > Will the implementation be very complex? Will using extensions directly take longer than modifying code? It might, so if it's a very small modification, it's not recommended to use; if the number of modifications is uncertain, the safety and consistency of the modifications need to be guaranteed, and the implementation is repeated, then it's best to give it a try first.

- Extensions also have a `public area`, displaying shared `actions`, `code snippets`, and `custom rule functions`. Everyone can also search for similar functionality and directly call or copy it and use it.
- Now let's discuss the scenarios where this extension can be used.

## DEFINITION
- **Action**: Execution unit, all file modifications are performed within the action.

- **Custom rules**: It can be understood as a general language designer for the principle diagram (https://angular.io/guide/schematics).

![delete_node_demo](https://cdn.jsdelivr.net/gh/wszgrcy/code-recycle@1.0.2/doc/en-US/image/delete_node_demo.jpg)

![custom_rule_demo](https://cdn.jsdelivr.net/gh/wszgrcy/code-recycle@1.0.2/doc/en-US/image/custom_rule_demo.jpg)

## Usage scenario
### Initialize project/module

- When initializing a project generally, we will refer to previous projects or other people's projects. At this time, if we want to use some part of the code in our own project, it is usually copied and then modified.
- At this time, there will be a problem: what should we do if the code we are using is updated? We may need to manually modify it again?
- This extension can directly cut the project files and add multiple files to the `action`, supporting file synchronization and conflict resolution.
- Specifying the different file positions to call the `action` can initialize the entire project or initialize a specific function module.

![action](https://cdn.jsdelivr.net/gh/wszgrcy/code-recycle@1.0.2/doc/en-US/image/action.jpg)

### Dynamic code snippets


- In general, most `code snippets` are generated with fixed code, which can solve the repetition of code writing.
- However, sometimes the implementation logic requires declarations/registrations/references before calling, which makes the `code snippets` impossible to implement.
- The `code snippets` only generate code for the current file and the current cursor position; they cannot cross files or insert code into a specific file at a specific position (although we actually need it, it cannot be achieved).
- This extension allows you to call the `code snippets` and pass the context to the action, generate the corresponding code, and insert it into the corresponding position through the `custom rules`.
> You can define a `trigger.xx.yy` pattern like this (regular expression matching), and pass `xx`, `yy` to the `action`, then generate related code through the `action`.

![snippet](https://cdn.jsdelivr.net/gh/wszgrcy/code-recycle@1.0.2/doc/en-US/image/snippet.jpg)

### Code Refactoring/Upgrading/Migrating
- This workload is often large, usually some repetitive labor, but very low-tech problems; only a few cases need treatment, but sometimes a large amount of repetitive work leads to operation errors debugging, which takes a lot of time; and sometimes at the end of the modification, it is found that the plan is not feasible and needs to be redone the code
- The custom rules in this extension, simply put, are **syntax query=>replace tool**, However, the accuracy of the syntax search is much higher than that of  search and replacement,  regular expression search and replacement.

- Through the implementation of various language's `CSS selector queries`, it allows compatibility of different languages with the same query specification and includes a `AST debugging tool` to ensure the query meets the expected results.

![ast](https://cdn.jsdelivr.net/gh/wszgrcy/code-recycle@1.0.2/doc/en-US/image/ast.jpg)



### Data Extraction
- When code needs to be internationalized, some parts of the strings need to be extracted, centralized translated, and then called through special internationalization functions.
- This extension can extract the specified data through `syntax queries` and translate it after completion, then replace the specified data in the original string, as the positioning of the `selector` is not changed, the replaced position found is bound

## Features
### Convenience
- Can be added quickly to any project
- File cutting is more convenient
### Interactivity
- Input variables
- Solution for template conflicts
### Atomicity
- Each action execution will be created in **VFS**, only all operations are successful before they are written to the file
- Dryrun mode, you can output the modified content to the console after execution, debugging completely normal before modification mode is written to the file
### Composition
- Different projects can be combined into one action
- Actions can refer to other actions
### Generalizability
- Language independence, framework independence, as long as there is an appropriate parser for the corresponding language, you can use it

---

## Related resources

- [https://www.bilibili.com/video/BV1Nb4y1u7FP/](https://www.bilibili.com/video/BV1Nb4y1u7FP/) - Introduction to the extension video
- [https://www.bilibili.com/video/BV1Vj411J7VZ/](https://www.bilibili.com/video/BV1Vj411J7VZ/) - Some demonstration of the extension usage
- [https://github.com/wszgrcy/code-recycle](https://github.com/wszgrcy/code-recycle) The current repository for saving i18n, which will also be open-sourced in the future.
- [vscode marketplace](https://marketplace.visualstudio.com/items?itemName=LDXCODE.code-recycle)
## Other
### Can it run offline?
- After the action/code snippet is executed for the first time, it will perform local caching. Subsequent calls will not depend on the server.
- You can force refresh and clear the cache.
- Future implementation will be pure single machine version.
### Why it's not open-sourced currently?
- Although the current extension is free to use and will not charge for existing features in the future, ultimately we want to use this extension to make money. However, we are not sure how to monetize it at the moment. If someone has a better idea, please feel free to contact me.
