## Callback Snippet

- Automatically take effect after adding code snippets


![调用静态代码片段](../zh-Hans/image/调用静态代码片段.png)
![动态代码片段配置](../zh-Hans/image/动态代码片段配置.png)
![调用动态代码片段](../zh-Hans/image/调用动态代码片段.png)

## Dynamic Placeholder
- When using dynamic snippets, since regex matching cannot predict, if the prefix word is matched after the input process parameter is not completely inputted and no snippets are matched, Dynamic Placeholder will appear. Dynamic Placeholder does not perform any operations, and when the input is completed, the matched snippets will display normally as placeholders.

![代码片段-动态填充](../zh-Hans/image/代码片段-动态填充.png)

## Configuration

- `code-recycle.snippet.triggerCharacters` Some trigger words for the callback snippet, the default is `['.']`