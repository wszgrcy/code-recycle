## 语法查询
- 支持400+种语法解析器;均可以使用CSS选择器风格进行节点查询
- 实现了[CSS 选择器](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_selectors)的大部分功能



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
- `:like(xxx)` 在`selector`模式中调用[like模式](./like.md)

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

