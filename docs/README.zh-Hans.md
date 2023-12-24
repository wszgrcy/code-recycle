## 一个快速创建`代码片段`,`脚手架`,`原理图`的设计器

## `快速初始化项目`,`脚手架层叠`,`可编程输入逻辑`,`动态代码片段`,`代码级依赖注入`

---

## 快速开始

- 需要先登录才能使用以下功能
  > 如果没有帐号需要先注册. 命令 `register`  
  > 登录. 命令 `login`
- 先进行`设计`需要的功能,再进行`调用`

## 设计

### 模板

- 在`编辑器`中,通过右键`裁剪`代码;在`文件管理器`中,右键文件/文件夹添加到模板
  ![template](https://cdn.jsdelivr.net/gh/wszgrcy/code-recycle@1.0.0/doc/image/template.webp)

#### 通用-替换值

- 选中内容会在生成时被替换
  > 如选中`world`=>`hello {{input}}`,调用动作时出现交互,输入`world`,并替换为`hello world`
- 支持`upcase`,`downcase`,`capitalize`,`camelcase`,`pascalcase`,`kebabcase`对输入进行格式化,如`{{upcase xxx}}`,输入变量后,会对变量进行大写化
  > 支持简写,如:`up`=>`upcase`

#### 通用-条件

- 选中内容会在生成时变为可选
  > 可以在配置页面增加不可选时默认值
- 调用动作时会有交互提示

#### 通用-选中/排除

- 选中内容会在生成时添加/排除到模板中
  > 默认为全部

#### 语言-选中/排除

- 与`通用`中的`选中/排除`类似,但是允许交互性的确定范围

#### 内容反选/正选

- 选中的内容在生成时为排除还是选中
  > 默认为正选

#### 高亮

- 查看该模板进行了哪些处理

#### 更新内容

- 当文件更新时,更新该文件`裁剪`操作的范围
- 更新后需要检查更新范围是否正确.

#### 预览

- 查询处理好的裁剪内容
  > 即将会被作为模板使用时,生成的内容

### 代码片段

- 创建代码片段
  > 命令 `create-snippet`
- 选择处理好的模板部分内容或直接自定义内容

#### 动态代码片段

- 支持插入`代码片段`后调用动作
- 支持传入`选中文件内容`,`插入代码片段内容`到动作
- 当使用代码片段自身的 `${1:}`语法与`{{1}}`正则匹配插入时.写法如下`${1:{{1~}}}`
  > 目前的一个设计问题,未来会修改

### 动作

- 创建动作
  > 命令 `create-action`
- 添加`文件模板`,`纯文件模板`,`动作嵌套`,`自定义`规则

![conflict-resolve](https://cdn.jsdelivr.net/gh/wszgrcy/code-recycle@1.0.0/doc/image/conflict-resolve.webp)

![custom-rule](https://cdn.jsdelivr.net/gh/wszgrcy/code-recycle@1.0.0/doc/image/custom-rule.webp)

#### 自定义规则-上下文

- 自定义规则是图灵完备的
  > [图灵完备演示视频](https://www.bilibili.com/video/BV19w411b7qx/)
- `选中文件/文件夹路径`,`当前工作空间文件夹路径`
- 如果被`代码片段`调用,还有`选中内容`,`插入内容`,`参数`

### ast 视图调试器

- 位于`编辑器`标题栏右上角
- 用于`自定义规则`选择节点时进行可视化调试
  ![ast-tree](https://cdn.jsdelivr.net/gh/wszgrcy/code-recycle@1.0.0/doc/image/ast-tree.webp)

#### css 选择器泛语言查询

- 使用`css选择器`进行不同语言的节点查询
- 实现了[css 选择器](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_selectors)的大部分功能

| name             | Support                                                                                                                                                                                                  |
| ---------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Descendant`     | `*`,` `,`>`,`<`,`+`,`~`,`,`                                                                                                                                                                              |
| `Attribute`      | `[xx]`,`[xx=yy]`,`[xx^=yy]`,`[xx$=yy]`,`[xx*=yy]`,`[xx!=yy]`,`[xx~=yy]` , `[xx\|=yy]`                                                                                                                    |
| `Pseudo`         | `:not`,`:has`,`:is`,`:where`,`:first-child`,`:last-child`,`:only-child`,`:nth-child`,`:nth-last-child`,`:first-of-type`,`:last-of-type`,`:only-of-type`,`:nth-of-type`,`:nth-last-of-type`,`:raw`,`:use` |
| `Pseudo-element` | `::parent`, `::children(x)` ,`::xx`                                                                                                                                                                      |

#### 说明

- 自定义伪类`:raw`,用于查询当前节点`原始`的 value/tag 属性

  > xxx:raw([value=yyy]);此选择器使用场景比较极端.极少数情况下可能会被使用

- `::parent` 查询父级元素
- `::children(x)` 查询当前元素的第几个子级元素
- `::xx` 查询该语言自定义的子级元素
- 自定义伪类`:use` 与`:is`类似,但是可以查询兄弟和后代

#### 查询节点通用属性

- `index` 索引,代表当前节点处于父级的哪个位置
- `tag` 节点的标签
- `value` 该节点的文本
- `range` 该节点的位置
- `children` 该节点的子元素列表
- `type` 节点类型(node/token)

#### 支持语言/语法

- typescript(typescript)
- typescript(javascript)
- typescript(typescriptreact)
- typescript(javascriptreact)
- @angular/compiler(ng-html)
- @angular/compiler(html)
- htmlparser2(html)
- htmlparser2(xml)
- jsonc-parser(json)
- gsql-ast-parser(sql)
- @vue/compiler-dom(vue)

| @lezer     |        |       |          |
| ---------- | ------ | ----- | -------- |
| cpp        | css    | html  | java     |
| javascript | json   | lezer | markdown |
| php        | python | rust  | sass     |
| xml        |        |       |          |

| antl4                        |                             |                       |                             |                             |                             |
| ---------------------------- | --------------------------- | --------------------- | --------------------------- | --------------------------- | --------------------------- |
| abb                          | abnf                        | acme                  | adaparent/ada83             | adaparent/ada95             | adaparent/ada2005           |
| alef                         | algol60                     | alloy                 | alpaca                      | angelscript                 | antlrparent/antlr2          |
| apt                          | arangodb                    | argus                 | arithmetic                  | ASL                         | asmparent/asm6502           |
| asmparent/asm8086            | asmparent/asmMASM           | asmparent/asmZ80      | asmparent/masm              | asmparent/nasm              | asmparent/pdp7              |
| asmparent/ptx-parent/ptx-2.1 | asnparent/asn               | atl                   | b                           | basic                       | bcl                         |
| bibcode                      | Bicep                       | bnf                   | C                           | calculator                  | callable                    |
| caql                         | cayenne                     | clf                   | clojure                     | cmake                       | cobol85                     |
| CPP14                        | cql                         | cql3                  | creole                      | CSS3                        | csv                         |
| cto                          | cypher                      | Dart2                 | datalog                     | dcm                         | dice                        |
| doiurl                       | dot                         | edif300               | edn                         | elixir-parser               | erlang                      |
| esolangparent/brainflack     | esolangparent/cool          | esolangparent/dgol    | esolangparent/lolcode       | esolangparent/loop          | esolangparent/nanofuck      |
| esolangparent/snowball       | esolangparent/wheel         | EVMB                  | fasta                       | fdo91                       | fen                         |
| flowmatic                    | focal                       | fol                   | fortranparent/fortran77     | fortranparent/fortran90     | fusiontables                |
| glsl                         | gml                         | golang                | graphql                     | graphstream-dgs             | gtin                        |
| guitartab                    | html                        | http                  | hypertalk                   | ical                        | icon                        |
| inf                          | informix                    | infosapient           | iri                         | iso8601                     | istc                        |
| jam                          | janus                       | javaparent/java       | javaparent/java8            | javaparent/java20           | jsparent/javascript         |
| jpa                          | json                        | json5                 | karel                       | kirikiri-tjs                | kotlinparent/kotlin         |
| kuka                         | kquery                      | lambda                | lcc                         | less                        | lisa                        |
| lrc                          | ltl                         | Lua                   | Lucene                      | matlab                      | mckeeman-form               |
| memcached                    | metamath                    | metric                | microc                      | modelica                    | modula2                     |
| moo                          | morsecode                   | PowerQuery            | mps                         | muddb                       | mumath                      |
| muparser                     | newick                      | oberon                | oncrpc                      | orwell                      | p                           |
| pascal                       | pbm                         | pcre                  | pddl                        | pdn                         | peoplecode                  |
| pii                          | pl0                         | plucid                | ply                         | PMMN                        | postalcode                  |
| prolog                       | promql                      | propcalc              | properties                  | protobuf2                   | protobuf3                   |
| pythonparent/python3         | qif                         | quakemap              | racket-bsl                  | racket-isl                  | rcs                         |
| refal                        | restructuredtext            | rfc822parent/datetime | rfc822parent/rfc822         | domain                      | filter                      |
| robotwar                     | romannumerals               | ron                   | rpn                         | Corundum                    | rust                        |
| scotty                       | scss                        | semver                | sexpression                 | sgf                         | sharc                       |
| sieve                        | smalltalk                   | smiles                | smtlibv2                    | snobol                      | Solidity                    |
| sqlparent/athena             | sqlparent/derby             | sqlparent/drill       | sqlparent/hiveparent/hivev2 | sqlparent/hiveparent/hivev3 | sqlparent/hiveparent/hivev4 |
| sqlparent/mysql              | sqlparent/plsql             | sqlparent/trino       | sqlparent/tsql              | sqlparent/informix-sql      | stacktrace                  |
| stellaris                    | suokif                      | swift-fin             | szf                         | tcp                         | telephone                   |
| tiny                         | tinybasic                   | tinyc                 | tinymud                     | tl                          | tnt                         |
| trac                         | tsv                         | ttm                   | turing                      | turtle                      | turtle-doc                  |
| unicode/graphemes            | unreal_angelscript          | upnp                  | url                         | useragent                   | vb6                         |
| verilogparent/verilog        | verilogparent/systemverilog | vhdl                  | vmf                         | wavefront                   | webidl                      |
| wkt-crs-v1                   | wln                         | wren                  | xml                         | xpathparent/xpath           | xpathparent/XPath20         |

| tree-sitter       |            |        |                   |                 |               |
| ----------------- | ---------- | ------ | ----------------- | --------------- | ------------- |
| haskell           | javascript | php    | java              | c_sharp         | css           |
| cpp               | python     | c      | ruby              | go              | bash          |
| tsx               | json       | scala  | embedded_template | agda            | jsdoc         |
| tsq               | regex      | ocaml  | ocaml_interface   | dbscheme        | ql            |
| toml              | swift      | ada    | sosl              | soql            | apex          |
| capnp             | clojure    | cmake  | comment           | commonlisp      | cuda          |
| d                 | dockerfile | dot    | elixir            | elm             | elisp         |
| erlang            | fennel     | fish   | formula           | fortran         | gitattributes |
| gleam             | glsl       | gomod  | gowork            | graphql         | hack          |
| jq                | json5      | kotlin | lalrpop           | latex           | lean          |
| tablegen          | lua        | make   | markdown          | markdown_inline | meson         |
| nix               | objc       | org    | pascal            | pgn             | proto         |
| racket            | rasi       | re2c   | rego              | rst             | r             |
| scss              | sexp       | smali  | sourcepawn        | sparql          | sql_bigquery  |
| ssh_client_config | svelte     | thrift | query             | turtle          | twig          |
| vue               | wat        | wast   | wgsl              | yaml            | yang          |

- `tree-sitter`需要拉取`https://github.com/wszgrcy/tree-sitter-wasm-bundle`仓库或根据格式自定义;然后将本地路径写入到配置`code-recycle.parser.tree-sitter.repository`中
---

## 调用

### 动作

- 在`文件管理器`中选择文件/文件夹右键调用
- 在`编辑器`中执行命令`callActionByFile`调用
- 在`视图`中交互执行动作
  > 通过自定义规则设计交互视图并使用

![custom-interactive](https://cdn.jsdelivr.net/gh/wszgrcy/code-recycle@1.0.8/doc/image/custom-interactive.jpg)

### 代码片段

- 定义后直接使用

# 支持

| System  | Support | test |
| ------- | ------- | ---- |
| Windows | [x]     | [x]  |
| Linux   | [x]     | [x]  |
| OSX     | [x]     | [x]  |

| Software | Support |
| -------- | ------- |
| Vscode   | [x]     |

# 项目代码包含

| Function              | Include |
| --------------------- | ------- |
| I18n                  | [x]     |
| Configuration WebView |         |
| Extension             |         |

# 其他

## 关于开源

- 在开发者能够维持自身的生存体征并保证有足够的精力进行插件开发前,暂时不开源
- 当开发者能从此插件中产生盈利并能维持自身生活需要时,会进行开源
- 目前本插件没有任何盈利行为
- 如果你有什么比较好的商业化想法,也可以联系我`wszgrcy@gmail.com`
