(x): Not recommended for use;(!): Warning message;[editor]: Can only be run in the editor, not in the CLI;
## call.functionBlock
- Call other scripts

### Parameters
| Optional | Enum | Default | Description |
|-|-|-|-|
|✓|||Script path|
|×|||Parameter array, parameter is `(arg)=>any` format|

### Return
- The value of the last line in the statement.


---

## call.blockTransformPipe
- (x)Call block

### Parameters
| Optional | Enum | Default | Description |
|-|-|-|-|
|×||||

### Return
- The last block value.


---

## read.contentResolveByFileQueryBlock
- Mapping file names and selectors to query file content to determine files, create content parser;

Outer query refers to when there are no matching files in a folder, it queries the parent folder and eventually finds the Workspace.

### Parameters
| Optional | Enum | Default | Description |
|-|-|-|-|
|×|||Query mode, 0: Current; 1: Continuously expanding out (if no query is found).|
|✓|||File Pattern|
|✓|||selector match|
|×|||Parser Configuration|
|✓||true|Is this a multiple choice?|
|✓|||Ignore list|

### Return
- {path?: string(path),
content: string(file content),
resolve$$: any(parser, internal using)}Object/Object Array


---

## read.contentResolveByFilePathBlock
- Based on the passed file path (array), read the file, and create a content parser.

### Parameters
| Optional | Enum | Default | Description |
|-|-|-|-|
|×|||File Path|
|×|||Parser Configuration|

### Return
- {path?: string(path),
content: string(file content),
resolve$$: any(parser, internal using)}Object/Object Array


---

## read.contentResolveByStringBlock
- Create a content parser based on the incoming string.

### Parameters
| Optional | Enum | Default | Description |
|-|-|-|-|
|×|||Content|
|×|||Parser Configuration|

### Return
- {path?: string(path),
content: string(file content),
resolve$$: any(parser, internal using)}


---

## read.editorInputBlock
- Read data input from text editor

### Parameters
| Optional | Enum | Default | Description |
|-|-|-|-|
|✓||selectRange|[editor]Reading the input data in the text editor.|

### Return
- oneof insertRange?: { value: string; range: [number,number] }[];
selectRange?: { value: string; range: [number,number] }[];
path: string;
dir: string;
workspacePath: string;
snippetParameters?: Record<string,any>;
trigger?: string


---

## read.fileBlock
- Read the specified file and try parsing (only supports JSON).

### Parameters
| Optional | Enum | Default | Description |
|-|-|-|-|
|×|||Read the content of the file.|
|×|json|plain|buffer||Formatting|

### Return
- string||object||buffer


---

## read.functionParameter
- Read the parameters from the external script (the parameters defined in the `call.functionBlock`)

### Parameters
| Optional | Enum | Default | Description |
|-|-|-|-|
|✓|||Context|
|×|||Variable name|

### Return
- saved data


---

## read.dropdown
- (x)Read the dropdown options

### Parameters
| Optional | Enum | Default | Description |
|-|-|-|-|
|✓||||

### Return
- Choose a value


---

## read.setting
- Read some settings of the platform.

### Parameters
| Optional | Enum | Default | Description |
|-|-|-|-|
|×|||Configuration Name|


---

## context.readParameterBlock
- (x)Read the context parameters, process them, and then write them into the data variables.

### Parameters
| Optional | Enum | Default | Description |
|-|-|-|-|
|×||||

### Return
- According to save


---

## context.setParameter
- (x)Set context parameters

### Parameters
| Optional | Enum | Default | Description |
|-|-|-|-|
|×||||
|✓||||

### Return
- According to the input


---

## function.defineBlock
- (x)Define an inline function; context parameters [item]: called when passed in; context parameters [input]: defined when passed in.

### Parameters
| Optional | Enum | Default | Description |
|-|-|-|-|
|✓||||
|×||||

### Return
- Function


---

## function.callBlock
- (x)Call inline function

### Parameters
| Optional | Enum | Default | Description |
|-|-|-|-|
|×||||
|✓||||

### Return
- The value of the last line in the statement.


---

## query.nodeQuery
- use "content resolve variable",use css style statement query node

### Parameters
| Optional | Enum | Default | Description |
|-|-|-|-|
|×|||Content parser, which returns the content by using contentResolveByFileQueryBlock/contentResolveByFilePathBlock/ contentResolveByStringBlock.|
|×|||Selector|
|✓||true|Query All|

### Return
- {path?: string(path),
content: string(file content),
resolve$$: any(parser, internal using),
node: object(queryed node)}Object/Object Array


---

## map.data
- (x)Data mapping, creating objects or tuples by inheriting from existing nodes; often used for modifying existing nodes.

### Parameters
| Optional | Enum | Default | Description |
|-|-|-|-|
|✓||||
|×||||
|×|list|object|||
|✓||||

### Return
- object||array


---

## operator.replaceNode
- Modify the file; can be used to add/modify/delete content.

### Parameters
| Optional | Enum | Default | Description |
|-|-|-|-|
|×|||Modification List|
|×|||Get the file (using nodeQuery, if any, would be itself)|
|×|||Range|
|×|||change content|


---

## operator.deleteFile
- Delete file

### Parameters
| Optional | Enum | Default | Description |
|-|-|-|-|
|×|||File Path|


---

## operator.newFile
- Create a new file

### Parameters
| Optional | Enum | Default | Description |
|-|-|-|-|
|✓|||Input Object|
|×|||(obj) => filename; get filename from input object|
|×|||(obj) => Content; Get content from the input object|


---

## operator.renameFile
- Rename file

### Parameters
| Optional | Enum | Default | Description |
|-|-|-|-|
|✓|||Input Object|
|×|||(obj) => old_filename; get old_filename from input object|
|×|||(obj) => old_filename; get old_filename from input object|


---

## operator.callAction
- (x)Call the action, similar to nested actions, needs to specify the file folder where the action is to be called.

### Parameters
| Optional | Enum | Default | Description |
|-|-|-|-|
|✓||||
|×||||


---

## operator.insertSnippet
- [editor] Insert code snippet (can only be inserted into the current editor)

### Parameters
| Optional | Enum | Default | Description |
|-|-|-|-|
|×||||
|×||||


---

## operator.template
- Insert file list as template; file content can be string or Buffer.

### Parameters
| Optional | Enum | Default | Description |
|-|-|-|-|
|×|||Object List|
|×|||(obj) => filename; get filename from input object|
|×|||(obj) => Content; From input object; string/Buffer|
|✓||false|revoke|
|✓|||Merge Strategy;[editor]editor|


---

## operator.commandExec
- (x)Execute command

### Parameters
| Optional | Enum | Default | Description |
|-|-|-|-|
|×||||
|✓||||
|✓||||


---

## globalVariable.setStringByInteractive
- By interacting to set global variables, obtain strings.

### Parameters
| Optional | Enum | Default | Description |
|-|-|-|-|
|×|||{name: Variable Name, message: Prompt, force: Force} []|

### Return
- string


---

## globalVariable.setBooleanByInteractive
- By interacting to set global variables, obtain the true/false value.

### Parameters
| Optional | Enum | Default | Description |
|-|-|-|-|
|×|||{name: Variable Name, message: Prompt, force: Force} []|

### Return
- boolean


---

## globalVariable.setValue
- (!)Set global action variables; The parameter order of this method is wrong, it will be adjusted in the future.

### Parameters
| Optional | Enum | Default | Description |
|-|-|-|-|
|✓|||Value|
|×|||Variable name|


---

## globalVariable.getValue
- Obtain the global action variable

### Parameters
| Optional | Enum | Default | Description |
|-|-|-|-|
|×|||Variable name|


---

## string.template
- (!)(x)String template for text concatenation; input data is required through "input/input.xx"; e.g., a{{input}}b; if the input is "1", the output will be "a1b"; future updates may involve re-designing to support different templates.

### Parameters
| Optional | Enum | Default | Description |
|-|-|-|-|
|✓|||Variable Object|
|×|||Template|

### Return
- string


---

## array.slice
- (x)Array/String truncation, similar to Array.prototype.slice

### Parameters
| Optional | Enum | Default | Description |
|-|-|-|-|
|×||||
|×||||
|×||||

### Return
- array


---

## array.sort
- (x)Array sorting, supporting default sorting and multi-field sorting

### Parameters
| Optional | Enum | Default | Description |
|-|-|-|-|
|×||||
|✓||||
|✓||asc||

### Return
- array


---

## array.reverse
- (x)Reverse the array; same as Array.prototype.reverse

### Parameters
| Optional | Enum | Default | Description |
|-|-|-|-|
|×||||

### Return
- array


---

## array.flat
- (x)Flatten the array; same as Array.prototype.flat

### Parameters
| Optional | Enum | Default | Description |
|-|-|-|-|
|×||||
|✓||1||

### Return
- array


---

## array.find
- (x)Array query; multiple query methods; context parameters [item]: each item; context parameters [index]: each item index;

### Parameters
| Optional | Enum | Default | Description |
|-|-|-|-|
|×||||
|×||||
|×|some|every|find|findIndex|findLast|findLastIndex|||

### Return
- boolean | array item


---

## array.concat
- (x)Array Connection

### Parameters
| Optional | Enum | Default | Description |
|-|-|-|-|
|×||||

### Return
- array


---

## array.map
- (x)Array mapping; same as Array.prototype.map; context parameter [item]: each item; context parameter [index]: each item index;

### Parameters
| Optional | Enum | Default | Description |
|-|-|-|-|
|×||||
|×||||

### Return
- array


---

## array.join
- (x)Array connection; array=> string, same Array.prototype.join

### Parameters
| Optional | Enum | Default | Description |
|-|-|-|-|
|×||||
|✓||||

### Return
- string


---

## array.category
- (x)Array classification; According to the returned classification name, divide the array into different groups; Context parameters [item]: Each item; Context parameters [index]: Each item index.

### Parameters
| Optional | Enum | Default | Description |
|-|-|-|-|
|×||||
|×||||

### Return
- [Category name (string), original array type]


---

## array.filter
- (x)Array filtering; context parameters [item]: each item; context parameters [index]: each item index;

### Parameters
| Optional | Enum | Default | Description |
|-|-|-|-|
|×||||
|×||||

### Return
- array


---

## array.push
- (x)Add element

### Parameters
| Optional | Enum | Default | Description |
|-|-|-|-|
|×||||
|×|tail|head|index|||
|✓||||
|✓||||

### Return
- array


---

## array.pop
- (x)Delete element

### Parameters
| Optional | Enum | Default | Description |
|-|-|-|-|
|×||||
|×|tail|head|index|||
|✓||||

### Return
- array


---

## object.merge
- (x)Object Merge

### Parameters
| Optional | Enum | Default | Description |
|-|-|-|-|
|×||||

### Return
- object


---

## object.toList
- (x)Object => Array

### Parameters
| Optional | Enum | Default | Description |
|-|-|-|-|
|×||||

### Return
- [key, value][]


---

## nodeCommon.insertRange
- Get the insert range; convert the range of a node into the insert range, e.g., "node.range:[0,2]", return "[0,0]" or "[2,2]"

### Parameters
| Optional | Enum | Default | Description |
|-|-|-|-|
|×|||Parser|
|×|start|end||Insert before/after the node|

### Return
- [number,number]


---

## nodeCommon.getData
- Use the path to get the specified data from objects/arrays/nodes, such as "[0].a" to get the a attribute of the 0th element.

### Parameters
| Optional | Enum | Default | Description |
|-|-|-|-|
|×|||Input value|
|×|||Query path; Refer to lodash.get|

### Return
- Based on the query path


---

## common.function
- (x)Some general functions. If you need to pass multiple parameters, you need to set them manually.

### Parameters
| Optional | Enum | Default | Description |
|-|-|-|-|
|✓||||
|×||||
|×||||

### Return
- Most strings | Regexp


---

## common.boolean
- (x)Create true/false values

### Parameters
| Optional | Enum | Default | Description |
|-|-|-|-|
|×||||

### Return
- boolean


---

## common.regexp
- (x)Create a regular expression

### Parameters
| Optional | Enum | Default | Description |
|-|-|-|-|
|×||||
|✓||||

### Return
- Regexp


---

## common.or
- (x)||: True data;??: Does not contain null, undefined true data

### Parameters
| Optional | Enum | Default | Description |
|-|-|-|-|
|×|??||||||
|×||||

### Return
- True value data


---

## common.didYouMean
- The most similar string, with a default similarity score of 0.4

### Parameters
| Optional | Enum | Default | Description |
|-|-|-|-|
|✓|||Input value|
|×|||Match List|

### Return
- string || null


---

## number.arithemetic
- (x)Perform ordinary digital operations, support numbers and arrays

### Parameters
| Optional | Enum | Default | Description |
|-|-|-|-|
|×||||
|×|+|-|*|/|%|||
|×||||

### Return
- number|number[]


---

## number.numberInput
- (x)Create a digital or array

### Parameters
| Optional | Enum | Default | Description |
|-|-|-|-|
|×||||

### Return
- number|[number,number]


---

## compare.boolCompare
- (x)True value comparison; compare the input values with true/false values.

### Parameters
| Optional | Enum | Default | Description |
|-|-|-|-|
|✓||||
|✓||true||

### Return
- boolean


---

## compare.baseCompare
- (x)Basic Comparison; Comparison Order is "First Value" "Comparison Type" "Second Value"

### Parameters
| Optional | Enum | Default | Description |
|-|-|-|-|
|✓||||
|×|EQ|NEQ|LT|LTE|GT|GTE|||
|✓||||

### Return
- boolean


---

## compare.rangeCompare
- Array comparison; comparison order is "Input 1" "Comparison Type" "Input 1"

### Parameters
| Optional | Enum | Default | Description |
|-|-|-|-|
|×|||Input 1|
|×|contains|reverse-contains|intersection|equal|not-intersection||compare type|
|×|||Input 1|

### Return
- boolean


---

## compare.stringCompare
- (x)String Comparison; Comparison order is "First Value" "Comparison Type" "Second Value"

### Parameters
| Optional | Enum | Default | Description |
|-|-|-|-|
|×||||
|×|startsWith|endsWith|includes|equal|||
|×||||

### Return
- boolean


---

## compare.multiCompare
- (x)Multiple comparison results (values) and/or

### Parameters
| Optional | Enum | Default | Description |
|-|-|-|-|
|×||||&&|||
|×||||

### Return
- boolean


---

## compare.typeCompare
- (x)Type Comparison

### Parameters
| Optional | Enum | Default | Description |
|-|-|-|-|
|✓||||
|×|String|Array|Object|Number|Boolean|null|undefined|nullish|||

### Return
- boolean


---

## compare.not
- (x)Reverse the result

### Parameters
| Optional | Enum | Default | Description |
|-|-|-|-|
|✓||||

### Return
- boolean


---

## view.view
- (!) View definition statement, the last statement in the view action must be it (there is no limit in the script for this).

### Parameters
| Optional | Enum | Default | Description |
|-|-|-|-|
|✓||||


---

## view.grid
- [editor]: Grid Layout

### Parameters
| Optional | Enum | Default | Description |
|-|-|-|-|
|✓|||{config:{list:{x,y,fixed,cols:col length}}}|
|×|||(()=>Other components)[]|


---

## view.button
- [editor] button

### Parameters
| Optional | Enum | Default | Description |
|-|-|-|-|
|✓|||{label,color,type,fontSet}|
|×|||Function call|


---

## view.label
- [editor] Tags

### Parameters
| Optional | Enum | Default | Description |
|-|-|-|-|
|✓|||{label}|


---

## view.input
- [editor] Input

### Parameters
| Optional | Enum | Default | Description |
|-|-|-|-|
|×|||Bind global variable|
|✓|||Configuration;{label,placeholder,type:'input'|'textarea',color,fontSet}|


---

## view.checkbox
- [editor] Checkbox

### Parameters
| Optional | Enum | Default | Description |
|-|-|-|-|
|×|||Bind global variable|
|✓|||{label,type:''|'icon',color,fontSet:图标集,labelPosition:'before'|'after'}|


---

## view.select
- [editor] Selection

### Parameters
| Optional | Enum | Default | Description |
|-|-|-|-|
|×|||Bind global variable|
|✓|||Configuration;{label,placeholder,type:'input'|'textarea',color,fontSet,multiple,preset,presetName:'queryMode'|'languageConfig'|'dataType'|'arrayAddType'}|
|✓|||List|
|×|||Display mapping function|
|×|||Value mapping function|


---

## view.showData
- [editor] Showing Data

### Parameters
| Optional | Enum | Default | Description |
|-|-|-|-|
|×|||Bind global variable|
|✓|||{type:'node-list'|'other'}|
|✓|||Showcasing Data|


---

## error.throw
- Throw an exception

### Parameters
| Optional | Enum | Default | Description |
|-|-|-|-|
|✓||||


---

## os.gitClone
- Retrieve specific files from a specified repository using Git; do not store account passwords in URLs.

### Parameters
| Optional | Enum | Default | Description |
|-|-|-|-|
|×|||url|
|✓||*|Match, refer to https://git-scm.com/docs/git-sparse-checkout#_internalsfull_pattern_set|
|✓|||# Repo folder path|
|✓||branch|Pattern|
|✓|||commit|

### Return
- {[filename]:Buffer}


---

## debug.dialog
- Debugging will display the input data in the modal pop-up.

### Parameters
| Optional | Enum | Default | Description |
|-|-|-|-|
|✓||||
|✓||||

### Return
- Input value


---

## debug.output
- Debugging will display the input data in the output channel below.

### Parameters
| Optional | Enum | Default | Description |
|-|-|-|-|
|✓||||
|✓||||

### Return
- Input value


---
