## 代码补全时
- 在`script.dir`文件夹内创建`snippet`并进入
- 在`manifest.json`写入补全代码配置
- [实例](https://github.com/wszgrcy/code-recycle-plugin-script/tree/master/snippet)
## 补全配置
```ts
interface SnippetSaveData {
  enable?: boolean;
  /** 前缀 */
  prefix: string[];
  /** 补全内容 */
  body: string;
  /** 语言列表 */
  languageList?: string[];
  name?: string;
  /** 正则匹配文件名 */
  pattern?: string;
  description?: string;
  /** 脚本名 */
  script?: string
  /** 给脚本传入参数 */
  parameters?: Record<string, any>;
  /** 正则匹配参数  */
  regexp?: {
    pattern: string;
    flag: string;
  };
}
```

## 相关调用
- [文档](api-docs/classes/Util.html#rule ':ignore')
- 使用`rule.editorInput`读取相关配置
- 使用`insertSnippet`手动触发插入代码片段
> 可以将`body`设置为` `(空白字符串占位)来调用

