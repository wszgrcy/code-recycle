## Config
- [Document](/api-docs/interfaces/Config.html ':ignore')

### Parser
- The parser in `antlr4` and `tree-sitter` is not included in the installed package by default, and will be automatically downloaded when used.
- When using the command line interface (CLI), it will默认 use the Node Package Manager (npm) for downloading. You can change the download location to `download` and manually specify the download path.

```json
{
    "parserDownload":"download",
    "antlrParserDir":"/path/to/antlr4",
    "treeSitterParserDir":"/path/to/tree-sitter"
}
```


### Default parser
- You can use the `code-recycle extnameList` configuration to view the default settings for determining the language of a file based on its file extension.
- If you want to modify the default configuration, you can modify the `parserMap` item to achieve it.

```json
{
    "parserMap":{".js":{"use":"antlr4","language":"javascript"}}
}
```

- You can use the `code-recycle parserList` to view all the supported parsers.

?> You can also manually specify the parser at the file query layer.

### git clone Repository location
- When using Git to clone the repository, it will be defaulted to saving the files to the system's temporary file folder.
- `gitCloneTmpDir` Manually specify the folder.

```json
{
    "gitCloneTmpDir":"/path/to/gitClone"
}
```

### Path
- The resolve of all relative paths in the script is based on `--cwd`,  Default is the same as the terminal.
- When performing a fuzzy search, `--root` controls the maximum boundary of the search, Default is the same as the  `--cwd`.

?> When using `ignore`, it will detect if the parent folder has ignored the files, and search up to `--root`.  

?> In VSCode editor, `--cwd` is the selected file for execution, and `--root` is the current working directory of the editor.


### Internationalization
- By default, it will be determined according to the system's terminal language. If the displayed language is incorrect, you can manually specify `CR_LANG=en/cn`.