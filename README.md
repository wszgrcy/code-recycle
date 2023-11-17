## A designer for quickly creating `code snippet`, `Scaffold Cascade`, and `Schematic diagram`.

## `Quickly initialize the project`,`Stackable layer structure`,`Programmable input logic`,`Dynamic code snippets`,`Code-level dependency injection`

---

| [中文](https://github.com/wszgrcy/code-recycle/blob/main/doc/README.zh-Hans.md) |
| ------------------------------------------------------------------------------- |

## Quick Start

- You need to log in first to use the following features
  > If you don't have an account, you need to register. Command `register`  
  > Log in. Command `login`
- First, `design` the functions needed for the call, and then make the `call`.

### Design

### Template

- `In the editor`, right-click and `cut` the code; in the `file manager`, right-click the file/folder and add it to the template
  ![template](https://cdn.jsdelivr.net/gh/wszgrcy/code-recycle@1.0.0/doc/image/template.webp)

#### Common - Replace Value

- Select the content will be replaced when generating
  > For example,select `world`=>`hello {{input}}`,When the call `action` is triggered, Enter world for the input and it will be replaced by hello world.
- Support for `upcase`, `downcase`, `capitalize`, `camelcase`, `pascalcase`, `kebabcase` to format the input, such as `{{upcase xxx}}`, after the variable is input, it will be capitalized.
  > Support abbreviations, such as: `up`=>`upcase`.

#### Common - Conditional

- Select the content will become optional when generated
  > You can add the default value in the `configuration page`
- Call `action` will have interactive prompts

#### Common - Select/Exclude

- Select the content will be added/excluded in the template
  > Default is all

#### Language - Select/Exclude

- Similar to the `common`中的`select/exclude`, but allow interactive determination of the range

#### Content - Invert/Select

- The content of the selected will be excluded or included in the template
  > Default is Select

#### Highlight

- View the templates that have been processed

#### Update Content

- When the file is updated, update the scope of the `cut` operation for the file.
- After updating, check if the update scope is correct.

#### Preview

- Query the processed `cut` content.
  > The generated content will be used as a template.

### Code Snippet

- Create `Code snippet`
  > Command `create-snippet`
- Select treated template parts or create content directly

#### Dynamic Code Snippet

- Insert `code snippet` and call actions
- Support `the input of chosen file content` and `insert code snippet content` into the action.
- When using the `${1:}` syntax of the code snippet itself and `{{1}}` regular expression match insert, the writing method is like this: `${1:{{1~}}}`
  > Currently a design problem, will be modified in the future.

### Action

- Create `Action`
  > Command `create-action`
- Add `file template`, `pure file template`, `action nested`, `custom` rules

![conflict-resolve](https://cdn.jsdelivr.net/gh/wszgrcy/code-recycle@1.0.0/doc/image/conflict-resolve.webp)

![custom-rule](https://cdn.jsdelivr.net/gh/wszgrcy/code-recycle@1.0.0/doc/image/custom-rule.webp)

#### Custom Rule - Context

- `Chosen file/folder path`, `Current workspace folder path`
- If called by the `Code Snippet`, there are `chosen content`, `inserted content`, and `parameters`.

### AST View Debugger

- Located in the right upper corner of the editor's title bar.
- Used for visual debugging when selecting `custom rule`

![ast-tree](https://cdn.jsdelivr.net/gh/wszgrcy/code-recycle@1.0.0/doc/image/ast-tree.webp)

#### CSS Selector Universal Language Query

- Use `css selector` for different language node queries
- Implement the majority of the [CSS selector](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_selectors) functions

| name             | Support                                                                                                                                                                                           |
| ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Descendant`     | `*`,` `,`>`,`<`,`+`,`~`,`,`                                                                                                                                                                       |
| `Attribute`      | `[xx]`,`[xx=yy]`,`[xx^=yy]`,`[xx$=yy]`,`[xx*=yy]`,`[xx!=yy]`,`[xx~=yy]` , `[xx\|=yy]`                                                                                                             |
| `Pseudo`         | `:not`,`:has`,`:is`,`:where`,`:first-child`,`:last-child`,`:only-child`,`:nth-child`,`:nth-last-child`,`:first-of-type`,`:last-of-type`,`:only-of-type`,`:nth-of-type`,`:nth-last-of-type`,`:raw` |
| `Pseudo-element` | `::parent`, `::children(x)` ,`::xx`                                                                                                                                                               |

#### Description

- Custom pseudo-classes `:raw`: used to query the `original` value/tag attribute of the current node

  > xxx:raw([value=yyy]); this selector is used in very extreme scenarios and is used only in a few cases.

- `::parent`: query the parent element
- `::children(x)`: query the xth child element of the current element
- `::xx`: query the custom child element defined in the current language.

#### Query general attributes of a node

- `index`: Index representing the position of the current node in its parent.
- `tag`: Label of the node.
- `value`: Text of the current node.
- `range`: Position of the current node.
- `children`: List of child elements of the current node.
- `type`: Type of the node (node/token).

#### Supported Language/Grammar

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

---

## Call

### Action

- Select file/folder right-click in the `File Manager` to call
- Execute command `callActionByFile` in the `Editor`

### Code snippet

- Define and use directly

# Support

| System  | Support | test |
| ------- | ------- | ---- |
| Windows | [x]     | [x]  |
| Linux   | [x]     | [x]  |
| OSX     | [x]     | [x]  |

| Software | Support |
| -------- | ------- |
| Vscode   | [x]     |

# The project code contains

| Function              | Include |
| --------------------- | ------- |
| I18n                  | [x]     |
| Configuration WebView |         |
| Extension             |         |

# Other

## About open source

- Before developers can maintain their livelihood and ensure sufficient energy to develop the plugin, the plugin will not be open-source temporarily.
- When developers can make a living from the plugin and maintain their lives, we will consider open-sourceing.
- Currently, the plugin has no commercial earnings.
- If you have better ideas for commercialization, please contact me at any time:`wszgrcy@gmail.com`
