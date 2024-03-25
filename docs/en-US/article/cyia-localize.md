# I separated localization from Angular:`@cyia/localize`
- Recently, while developing the VSCode Extension, I discovered an issue where the plugin and WebView sections sometimes share a portion of the code, which happens to contain content that needs to be translated, resulting in the inability to use the l10n provided by VSCode itself
- Because some of the WebView pages were developed using Angular, it would be best if a translation could be used for implementation. Therefore, I came up with the `localize` in Angular to separate modules and make them a universal dependency

## How to use it?
- [access the usage documentation](https://github.com/wszgrcy/cyia-localize/blob/main/readme.zh-Hans.md)

## How to separate?
- With the experience of [separating dependency injection](https://wszgrcy.github.io/code-recycle/#/en-US/article/static-injector) , is actually quite simple because it is an independent module, so just find the introduction and extraction parts
- The import section is exported intact, while the extraction section uses some self implemented code. However, the related ID generation algorithm remains the same, which means that the translation in Angular can be directly moved here for use

## Synchronize updates
- Due to the limited number of `localize` changes, only a small portion has been modified
- Using [Sync Script](https://github.com/wszgrcy/cyia-localize/blob/45cbb40e84191bf349c34239c4833a98a6f1116a/script/sync-localize.ts) And use `github actions` for update testing
```yml
      - uses: wszgrcy/code-recycle-action@main
        with:
          path: ./script/sync-localize.ts
          cwd: ./src
```

## Calling methods

```ts
import { $localize } from '@cyia/localize';
$localize`one`;
```
- Use `i18n ./src` Extract all `$localize` label template contents under `src` and generate `extract.json` metadata
  > Generate ID consistent with `@angular/localize`
- Copy `extract.json` custom language translation and write the translation content into the `target` field
- Use `i18n convert ./i18n-merge ./i18n` Convert translation metadata to `key-value` format for reference
- Custom reference format import translation, such as

```ts
// Node environment demonstration
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