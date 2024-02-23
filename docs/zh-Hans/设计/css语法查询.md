## 语法查询
- 支持400+种语法解析器;均可以使用CSS选择器风格进行节点查询
- 实现了[CSS 选择器](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_selectors)的大部分功能

![ast-view.png](../image/ast-view.png)
![ast-view-属性.png](../image/ast-view-属性.png)

## CSS 选择器支持

| name             | Support                                                                                                                                                                                                  |
| ---------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Descendant`     | `*`,` `,`>`,`<`,`+`,`~`,`,`                                                                                                                                                                              |
| `Attribute`      | `[xx]`,`[xx=yy]`,`[xx^=yy]`,`[xx$=yy]`,`[xx*=yy]`,`[xx!=yy]`,`[xx~=yy]` , `[xx\|=yy]`                                                                                                                    |
| `Pseudo`         | `:not`,`:has`,`:is`,`:where`,`:first-child`,`:last-child`,`:only-child`,`:nth-child`,`:nth-last-child`,`:first-of-type`,`:last-of-type`,`:only-of-type`,`:nth-of-type`,`:nth-last-of-type`,**`:raw`**,**`:use`**,**`:like`**,**`:infer`**|
| `Pseudo-element` | `::parent`, `::children(x)` ,`::xx`                                                                                                                                                                      |

### 说明


  > xxx:raw([value=yyy]);此选择器使用场景比较极端.极少数情况下可能会被使用

- `::parent` 查询父级元素
- `::children(x)` 查询当前元素的第几个子级元素
- `::xx` 查询该语言自定义的子级元素

#### 自定义伪类
- `:raw`,用于查询当前节点`原始`的 value/tag 属性
- `:use` 与`:is`类似,但是可以查询兄弟和后代
- `:infer(xxx)` 将匹配到的节点保存到`infer`对象中,保存的名字为`xxx`
- `:like(xxx)` 在`selector`模式中调用[like模式](./like查询.md)

### 查询节点通用属性

- `index` 索引,代表当前节点处于父级的哪个位置
- `tag` 节点的标签
- `value` 该节点的文本
- `range` 该节点的位置
- `children` 该节点的子元素列表
- `type` 节点类型(node/token)

### 举例
以上面的`ast view`截图为准

- `VariableDeclaration`=>查询tag=`VariableDeclaration`的节点
- `VariableDeclaration:has(VariableDefinition[value=a])`=>查询`VariableDeclaration`的子节点中有`VariableDefinition`标签,并且内容(value)为`a`
- `VariableDeclaration::children(0)`=>查询`VariableDeclaration`节点的第0个子节点=>`let`
- `let:use(*,+VariableDefinition)`=> 查询`let自身和他的兄弟节点是VariableDefinition`
- `VariableDeclaration[name=VariableDeclaration]`=>查询`VariableDeclaration`节点中`name`属性为`VariableDeclaration`的节点

### 支持语言/语法

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

?> 在CLI中设置`treeSitterParserDir`