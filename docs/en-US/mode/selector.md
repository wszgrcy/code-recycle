## Syntax Query
- supports 400+ syntax parsers; all can be queried using CSS selector style
- Achieves most of the features of [CSS selectors](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_selectors)



## CSS Selector Support

| name             | Support                                                                                                                                                                                                  |
| ---------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Descendant`     | `*`,` `,`>`,`<`,`+`,`~`,`,`                                                                                                                                                                              |
| `Attribute`      | `[xx]`,`[xx=yy]`,`[xx^=yy]`,`[xx$=yy]`,`[xx*=yy]`,`[xx!=yy]`,`[xx~=yy]` , `[xx\|=yy]`                                                                                                                    |
| `Pseudo`         | `:not`,`:has`,`:is`,`:where`,`:first-child`,`:last-child`,`:only-child`,`:nth-child`,`:nth-last-child`,`:first-of-type`,`:last-of-type`,`:only-of-type`,`:nth-of-type`,`:nth-last-of-type`,**`:raw`**,**`:use`**,**`:like`**,**`:infer`**|
| `Pseudo-element` | `::parent`, `::children(x)` ,`::xx`                                                                                                                                                                      |

### Description

- Implements custom pseudo-class `:raw` to query the `origin` value/tag attributes of the current node

  > xxx:raw([value=yyy]); This selector has a very unusual use case and is only likely to be used in a few situations.
- `::parent` queries the parent element
- `::children(x)` queries the xth child element of the current element
- `::xx` queries a custom sub-element defined in the current language
- The custom pseudo-class `:use` is similar to `:is`, but can query brothers and descendants.

## query general attributes of nodes
- `index` index, representing the position of the current node in its parent
- `tag` tag of the node
- `value` text of the node
- `range` position of the node
- `children` child elements of the node
- `type` type of the node (node/token)

### Examples

The above `AST view` screenshot is used as the reference.

- `VariableDeclaration`=> Query nodes with tag `VariableDeclaration`
- `VariableDeclaration:has(VariableDefinition[value=a])`=> Query the child nodes of `VariableDeclaration` that have `VariableDefinition` tag and its content (value) is `a`
- `VariableDeclaration::children(0)`=> Query the 0th child node of `VariableDeclaration`=> `let`
- `let:use(*,+VariableDefinition)`=> Query the nodes that `let` itself and its sibling nodes are `VariableDefinition`
- `VariableDeclaration[name=VariableDeclaration]`=> Query the nodes in `VariableDeclaration` nodes that have `name` attribute as `VariableDeclaration`