# How to customize search logic in Visual Studio Code?
- Search/replace function, a feature available in every editor.
- mainly used for text replacement
- But in code development, sometimes there are too many search results, and it's not easy to filter out the suitable content.
- We often need to do a search/replace operation in a certain `block` or at a specific location in a specific logic (for example, the yth parameter name within the xx function).
- At this time, we need to customize our own search logic to meet the requirements.
## The custom view actions provided by Code Recycle.
- `Code Recycle` is an extension currently available in Visual Studio Code. It allows users to query content by specifying a grammar parser and perform related operations.
- It currently supports view display and allows users to customize the view to meet various content needs.
- Currently, a custom search logic action is provided right out of the box. Of course, you can also copy this action and modify it to suit your needs.

![custom-interactive](https://cdn.jsdelivr.net/gh/wszgrcy/code-recycle@1.0.8/doc/image/custom-interactive.jpg)
![demo](https://cdn.jsdelivr.net/gh/wszgrcy/code-recycle@1.0.9/doc/image/view-action/demo.gif)

### In addition to customizing the search, Code Recycle can also do other things.
- Initially, the extension was designed to make it more convenient to locate file content, **handle code-level repetitive logic**, and modify file content.
- Therefore, as long as the content to be processed **exists in logic**, it can be achieved using this extension. However, recently, support for custom views has been provided to make it easier for everyone to use.


---

## Other
## Where can I find it?
- `Currently`, it supports all systems and is now available on the [Microsoft Vscode Marketplace](https://marketplace.visualstudio.com/items?itemName=LDXCODE.code-recycle)  
- After installation and login, open the command panel and type `code-recycle` to enter the configuration; move into the public area and search for `interactive` to find the public area view action and add it; find the `Code Recycle` view in the sidebar, open it to select the action just added.

![add-custom-interactive](https://cdn.jsdelivr.net/gh/wszgrcy/code-recycle@1.0.9/doc/image/add-custom-interactive.jpg)

## Relevant resources
- [Video: How to customize search logic in Visual Studio Code?](https://youtu.be/-I4Zb36sesI)
- [Video: Initialize project - template generation is reversible](https://youtu.be/ci_daT_l04U?feature=shared)
- [Code Cycle: Turing Complete Implementation](https://youtu.be/nvoNm8Vr06c?feature=shared)
- [Quick development in Angular by using dynamic code snippets](https://youtu.be/9iG8E5gzguE) 
- [code-recycle-demo](https://youtu.be/41xOhQdWtlY)
- [https://www.bilibili.com/video/BV1Nb4y1u7FP/](https://www.bilibili.com/video/BV1Nb4y1u7FP/) - Introduction to the extension video
- [https://www.bilibili.com/video/BV1Vj411J7VZ/](https://www.bilibili.com/video/BV1Vj411J7VZ/) - Some demonstration of the extension usage
- [https://github.com/wszgrcy/code-recycle](https://github.com/wszgrcy/code-recycle) The current repository for saving i18n, which will also be open-sourced in the future.
- [vscode marketplace](https://marketplace.visualstudio.com/items?itemName=LDXCODE.code-recycle)