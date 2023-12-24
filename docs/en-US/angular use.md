# Angular uses dynamic code snippets for rapid development.

- Currently, in Angular, the related usage of directives/pipes/components, usually, we need to introduce (ts import && ng imports) and then call it; if it's the first time using, we also need to create.

- This development mode often interrupts our development thinking, because we need to create=>introduce=>use, constantly switching files and changing our thinking.

- So how can we change this approach to make the implementation of code as simple as dependency injection? Should we only consider using it and not consider other issues?

- This solution, which I call **Code-Level Dependency Injection** and the means to implement it, which I call **Dynamic Code Snippets** I'll elaborate on next.


## Use Code Recycle to implement dynamic code snippets.
- General code snippets: The content to be inserted at call time is already determined and can only be inserted into the current file.
- Dynamic code snippets: When inserted, it captures the relevant context and calls an **action** to handle other files, achieving **dependency injection**.
## Code Recycle provides some pre-trained Angular features that can be used immediately.
- `Code Recycle` has a **visual and programmable designer** that can generate various code based on `predetermined logic`.
> You can understand it as having a customizable principle diagram.

![custom_rule_demo](https://cdn.jsdelivr.net/gh/wszgrcy/code-recycle@1.0.2/doc/en-US/image/custom_rule_demo.jpg)

- Now, some **actions** and **dynamic code snippets** are also available for Angular developers to use.
> All content in the **public area** can be directly called or **modified** according to your usage habits.


### **[Dynamic code snippets]**: Automatic reference of directives/pipes in HTML.
- This action automatically searches for pipes and directives in the specified area, and if they exist, they will be referenced during the call. If they don't exist, it will create a empty implementation in the specified folder and then reference it.
![directive](https://cdn.jsdelivr.net/gh/wszgrcy/code-recycle@1.0.5/doc/image/dynamic-snippet-angular/directive.gif)
![pipe](https://cdn.jsdelivr.net/gh/wszgrcy/code-recycle@1.0.5/doc/image/dynamic-snippet-angular/pipe.gif)

### **[Dynamic code snippets]** reference 
- When executed, it will automatically insert `@ViewChild {{name}}:any` and import (if it doesn't exist) in the ts file.
![reference](https://cdn.jsdelivr.net/gh/wszgrcy/code-recycle@1.0.5/doc/image/dynamic-snippet-angular/reference.gif)

### **[Dynamic code snippets]** Automatic generation of methods/properties in HTML.
- When executed, it will automatically insert methods/properties in the ts file.
![cfn](https://cdn.jsdelivr.net/gh/wszgrcy/code-recycle@1.0.5/doc/image/dynamic-snippet-angular/cfn.gif)

### **[Dynamic code snippets]** material design
- When executed, it will insert relevant references (if they don't exist) and generate corresponding ts code (if necessary).
![mbutton](https://cdn.jsdelivr.net/gh/wszgrcy/code-recycle@1.0.5/doc/image/dynamic-snippet-angular/mbutton.gif)

#### column
- When this snippet is called, it will automatically insert the name into the `{{columnList}}` variable.
![mtable](https://cdn.jsdelivr.net/gh/wszgrcy/code-recycle@1.0.5/doc/image/dynamic-snippet-angular/mtable.gif)

### **[Action]** Component Template
- When executed, it will automatically create a component and the nearest module (Model || Standalone Component) and insert the corresponding imports.
> Similar to the Angular official schematics.

![template1](https://cdn.jsdelivr.net/gh/wszgrcy/code-recycle@1.0.5/doc/image/dynamic-snippet-angular/template1.webp)

---

## Other
## Where can I find it?
- `Currently`, it supports all systems and is now available on the [Microsoft Vscode Marketplace](https://marketplace.visualstudio.com/items?itemName=LDXCODE.code-recycle)  


## How do I use other languages/frameworks?
- Any language/framework can be used, but currently only Angular provides some pre-trained features that can be used immediately.
> That is,Extension developers have implemented the above content using the **designer** and made it available in the **public area**.
- Other languages/frameworks can refer to some existing **actions** and **code snippets** in the public area to implement what they need.

## Relevant resources
- [video_ENG_Subtitle](https://youtu.be/9iG8E5gzguE) Quick development in Angular by using dynamic code snippets.
- [video_ZH](https://www.bilibili.com/video/BV1wc411i7pZ/) Quick development in Angular by using dynamic code snippets.
- [code-recycle-demo](https://youtu.be/41xOhQdWtlY)
- [https://www.bilibili.com/video/BV1Nb4y1u7FP/](https://www.bilibili.com/video/BV1Nb4y1u7FP/) - Introduction to the extension video
- [https://www.bilibili.com/video/BV1Vj411J7VZ/](https://www.bilibili.com/video/BV1Vj411J7VZ/) - Some demonstration of the extension usage
- [https://github.com/wszgrcy/code-recycle](https://github.com/wszgrcy/code-recycle) The current repository for saving i18n, which will also be open-sourced in the future.
- [vscode marketplace](https://marketplace.visualstudio.com/items?itemName=LDXCODE.code-recycle)