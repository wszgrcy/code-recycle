# Initialize the project like building blocks? You can use the template function of Code Recycle.
- In general, when initializing a new project, we often use existing files to create a template (repository) for use.

- However, sometimes an update for a specific function (module) cannot be synchronized across all the file templates. We need to continue making adjustments after generating the templates.
- At this time, you can try using the module function of Code Recycle.

## The template function of Code Recycle that it possesses.
- Support interaction. You can input a string when calling to modify some variables in the file. You can choose options to control whether the content is generated.
![template-process](https://cdn.jsdelivr.net/gh/wszgrcy/code-recycle@1.0.6/doc/image/template/template-process.jpg)
![call](https://cdn.jsdelivr.net/gh/wszgrcy/code-recycle@1.0.6/doc/image/template/call.gif)

- Template update synchronization. When the linked file is updated, you can synchronize the file/project to keep the original file modification (replacement/optional) range.

> Use the diff algorithm to synchronize. If the position is not accurate after updating, you may need to manually correct it.

![sync](https://cdn.jsdelivr.net/gh/wszgrcy/code-recycle@1.0.6/doc/image/template/update.webp)
- Module composition. You can encapsulate the function into independent `actions`, and then call them together through action `nest`.
![nest](https://cdn.jsdelivr.net/gh/wszgrcy/code-recycle@1.0.7/doc/image/template/nest.webp)

- Template undo. You can reverse the contents of a `template` in a specific `action` by using the **diff editor**.
![cancel](https://cdn.jsdelivr.net/gh/wszgrcy/code-recycle@1.0.6/doc/image/template/cancel.webp)

---

## Other
## Where can I find it?
- `Currently`, it supports all systems and is now available on the [Microsoft Vscode Marketplace](https://marketplace.visualstudio.com/items?itemName=LDXCODE.code-recycle)  


## Relevant resources
- [Video: Initialize project - template generation is reversible](https://youtu.be/ci_daT_l04U?feature=shared)
- [Code Cycle: Turing Complete Implementation](https://youtu.be/nvoNm8Vr06c?feature=shared)
- [Quick development in Angular by using dynamic code snippets](https://youtu.be/9iG8E5gzguE) 
- [code-recycle-demo](https://youtu.be/41xOhQdWtlY)
- [https://www.bilibili.com/video/BV1Nb4y1u7FP/](https://www.bilibili.com/video/BV1Nb4y1u7FP/) - Introduction to the extension video
- [https://www.bilibili.com/video/BV1Vj411J7VZ/](https://www.bilibili.com/video/BV1Vj411J7VZ/) - Some demonstration of the extension usage
- [https://github.com/wszgrcy/code-recycle](https://github.com/wszgrcy/code-recycle) The current repository for saving i18n, which will also be open-sourced in the future.
- [vscode marketplace](https://marketplace.visualstudio.com/items?itemName=LDXCODE.code-recycle)