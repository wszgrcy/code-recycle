## How programmers encapsulate logic?
## Encapsulation
- Everyone knows that encapsulating code improves readability, makes code clearer, and makes it easier to maintain.
- What is encapsulation of logic? For example, if we want to modify a function's parameter in the example, change `foo(a,b)` to `foo(b,a)`, we can simply move `a` to the end of `b` or move `b` to the beginning of `a`. This is our logic when operating, and encapsulation of logic means replacing us performing this operation. We only need to call it, and it will have `someone` help us implement it.

## Why do we need to encapsulate logic?
- The example above only showed simple swapping of parameter positions. If we need to swap hundreds of parameters, it becomes problematic. If it's not swapping parameters, but rather more complex changes that need to be repeated hundreds of times, it's not only possible to make errors but also requires a lot of energy.

## We need to imitate the way people modify code.
- When modifying code, we know that this is a function/variable/expression, and we know that we need to modify a certain statement under a certain condition. So we start implementing it.
- Currently, we just need to find a tool that can parse the syntax to find the content and then modify/replace/delete it.

## Code Recycle has implemented syntax parsing, CSS-style queries, and content replacement.
- I have implemented an extension that interfaces with various parsing libraries currently available on the market. The current version supports the parsing of over [400+ syntaxes](https://wszgrcy.github.io/code-recycle/#/zh-Hans/%E8%AE%BE%E8%AE%A1/css%E8%AF%AD%E6%B3%95%E6%9F%A5%E8%AF%A2?id=%e6%94%af%e6%8c%81%e8%af%ad%e8%a8%80%e8%af%ad%e6%b3%95), covering about **99%** of commonly used languages and syntaxes
- It also has a unified CSS style query that allows everyone to use the same logic to query regardless of the language.
> :has  selects all nodes that satisfy a certain rule for the current node  
> :is  selects the current node that satisfies a certain rule  
> :use  selects the current node and other nodes that are selected through the current node  
> ::parent, ::children  selects the parent and children of the current node respectively  
> [... more](https://wszgrcy.github.io/code-recycle/#/zh-Hans/%E8%AE%BE%E8%AE%A1/css%E8%AF%AD%E6%B3%95%E6%9F%A5%E8%AF%A2?id=css-%E9%80%89%E6%8B%A9%E5%99%A8%E6%94%AF%E6%8C%81)
> The extension has implemented almost complete CSS syntax querying, so there is no need to worry about scenarios where there are no choices. If there are, you can contact me and I will provide a solution.


## Business scenarios
- For static use cases, such as initializing projects/functional modules, everyone can use templates. Whether it's self-made templates or direct use of Git templates, it is convenient.

![template](https://cdn.jsdelivr.net/gh/wszgrcy/code-recycle@1.1.0/docs/image/template.webp)
![gitClone](https://cdn.jsdelivr.net/gh/wszgrcy/code-recycle@1.1.0/docs/zh-Hans/image/gitClone.png)

- Some dynamic initialization in development, such as writing custom components into HTML content in front-end development, often need to be imported and declared in the code. Using dynamic code snippets can make it very convenient

![custom-interactive](https://cdn.jsdelivr.net/gh/wszgrcy/code-recycle@1.1.0/docs/image/custom-interactive.jpg)
![reference](https://cdn.jsdelivr.net/gh/wszgrcy/code-recycle@1.1.0/docs/image/dynamic-snippet-angular/reference.gif)

- To extract text for internationalization or other purposes, you can use the action to directly query and write files
- Code restructuring, such as moving parameters, logic migration, if you don't have confidence/pay attention to detail/have more than 10 minutes of direct modification, you can directly create the modification logic with the action to avoid modifying the time
- If you have some specific operations, such as advanced custom search, and need to repeat this operation repeatedly, you can use visual actions to design your search

![demo](https://cdn.jsdelivr.net/gh/wszgrcy/code-recycle@1.1.0/docs/image/view-action/demo.gif)

- In summary, as long as the thing you want to achieve does not require too much consideration, it is recommended to consider using this extension. It may bring you unexpected surprises for your development.

## Documents
- If you are interested and want to experience it, you can [read the documents](https://wszgrcy.github.io/code-recycle/#/en-US/README)