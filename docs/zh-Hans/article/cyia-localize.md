# 我从 Angular 中分离出来本地化:`@cyia/localize`
- 最近在做 VSCode Extension 开发的时候,发现一个问题,插件部分和 WebView 部分有时候会共用一部分代码,而这部分代码里又恰好有需要翻译的内容,这就导致 VSCode 本身提供的 l10n 没法使用
- 因为 WebView 部分页面是使用 Angular 开发,所以如果能用一种翻译实现是最好的了,所以我想到了 Angular 中的 `localize`,对分离模块,使其成为通用依赖

## 如何使用?
- [访问使用文档](https://github.com/wszgrcy/cyia-localize/blob/main/readme.zh-Hans.md)

## 如何分离?
- 有了[分离依赖注入](https://wszgrcy.github.io/code-recycle/#/zh-Hans/article/static-injector)的经验,其实这个已经很简单了,因为他是一个独立模块,所以只要把引入部分和提取部分找到就可以了
- 引用部分原封不动导出,提取部分使用了一部分自实现代码,但相关id生成算法仍然是一样的,也就是说在 Angular 中的翻译可以直接移动到这里使用

## 同步更新
- 由于`localize`部分改动不是很多,所以只修改了很少一部分.
- 使用[同步脚本](https://github.com/wszgrcy/cyia-localize/blob/45cbb40e84191bf349c34239c4833a98a6f1116a/script/sync-localize.ts)并使用`github actions`进行更新测试
```yml
      - uses: wszgrcy/code-recycle-action@main
        with:
          path: ./script/sync-localize.ts
          cwd: ./src
```

## 调用方法

```ts
import { $localize } from '@cyia/localize';
$localize`one`;
```

- 使用`i18n ./src` 提取`src`下所有`$localize`标签模板内容生成`extract.json`元数据
  > 与`@angular/localize` 生成 id 一致
- 复制`extract.json`自定义语言翻译,将翻译内容写入到`target`字段
- 使用`i18n convert ./i18n-merge ./i18n`将翻译元数据转换为`key-value`格式用于引用
- 自定义引用格式导入翻译,如

```ts
// node环境演示
import path from 'path';
import fs from 'fs';
import { loadTranslations } from '@cyia/localize';
export const LanguageMap: Record<string, string> = {
  zh_cn: 'zh-Hans',
  cn: 'zh-Hans',
  en: 'en-US',
  en_us: 'en-US',
};
export function loadI18n() {
  let lang = process.env['CR_LANG']?.toLowerCase();
  if (!lang) {
    if (process.env['LANGUAGE']) {
      lang = process.env['LANGUAGE'].split(':')[0].toLowerCase();
    } else if (process.env['LANG']) {
      lang = process.env['LANG'].split('.')[0].toLowerCase();
    }
  }
  let cache;
  const filePath = path.join(__dirname, `./i18n/${LanguageMap[lang!] || lang || 'zh-Hans'}.json`);
  if (ENV === 'test') {
    cache = {};
  } else {
    if (!fs.existsSync(filePath)) {
      cache = __non_webpack_require__('./i18n/zh-Hans.json');
    } else {
      cache = __non_webpack_require__(filePath);
    }
  }

  loadTranslations(cache);
}

loadI18n();
```