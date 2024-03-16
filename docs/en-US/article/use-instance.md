## How to accurately locate codes? - `Code Recycle`
- Programmers often rely on text search when querying code during the development process, although this is useful in most cases, it may not fully meet our needs

```ts
let a    =     1;let b=`let a=1`
```

- It is usually difficult to search for the above code statement `let a    =     1` because on one hand, there may be string interference, and on the other hand, the format may be different, making it impossible to directly determine the unique statement

- However, when we use `code cycle`, we can directly match this statement with `let a=1` because it is based on syntax trees for matching. One characteristic is that it is not sensitive to blank content, and the other is that all characters are treated as node content for querying
- In this way, we can use the same search content as before to match more accurate results

## Quickly exchange parameters?
- If you want to exchange the parameters of function calls, it may be a big project that requires checking each function call and manually handling the positions of the two parameters
- Would it be more convenient to exchange all the code with just a few lines of code?
- That's right, you can write it like this in `code cycle`

```ts
  {
    query: `CallExpression:like(test1( [[{^]] [[$p1]] [[...]] [[$p4]] [[$}]] ) )`,
    multi: true,
    replace: {
      p1: `{{''|ctxInferValue:'p4'}}`,
      p4: `{{''|ctxInferValue:'p1'}}`,
    },
   },
```

- The above demonstration involves exchanging the first and last parameters. If you have already determined the number of parameters, the writing method can be simpler

## Rewrite the parameter transfer structure?
- When there are changes in the design, it is usually necessary to modify the parameter transfer structure and place the previous parameters into the new structure
- At this point, you can do this

```ts
{
    query: `CallExpression:like(test1( [[{^]]  [[...]] [[$p4]] [[$}]] ) )`,
    multi: true,
    replace: {
      p4: `{value:{{''|ctxInferValue:'p4'}}}`,
    },
}
```

- The last parameter becomes an object, and the original parameter value will be in the object

## Other uses

- `console.[[$method:/log|info/]]()` Query the specified calling method for `console`
- `class [[$className]] { [[{]] test(){}  [[}]] }`Query classes containing test methods
- `{key:[[$value]]}`Query the value of the key

## More?
- The tool currently supports the execution of `CLI` and `VSCode Extension`
- The above example is an introduction to the basic usage of `code cycle` using the script language `typescript` as an example. The tool currently supports [over 400 languages/syntax parsing](https://wszgrcy.github.io/code-recycle/#/en-US/parser),You can view [document](https://wszgrcy.github.io/code-recycle/#/en-US/README) learn more
- If you want to see more instances, you can [visit the repository](https://github.com/wszgrcy/code-recycle-plugin-script) view and Run
- If you are already interested, you can [start quickly](https://wszgrcy.github.io/code-recycle/#/en-US/quickstart)