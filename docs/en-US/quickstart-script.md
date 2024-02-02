## Installation

- [Plugin Marketplace](https://marketplace.visualstudio.com/items?itemName=LDXCODE.code-recycle)
- Visual Studio Code marketplace

![Install](../zh-Hans/image/安装.png)

## Create a new script folder
- Choose a location to create a folder and create it in the following hierarchy


?> You can refer to the [Demo Repo](https://github.com/wszgrcy/code-recycle-plugin-script)


```tree
.
├── action 
│   ├── hello2.js
│   └── hello.js
├── snippet 
│   ├── hello2.js
│   └── manifest.json
└── view 
    ├── hello2.js
    └── hello.js
```

## Create Script
- Use the `editor` to open the created folder, then right-click to quickly create a script

![创建](./image/script/create-script.png)

![创建-输入名称](./image/script/create-script-name.png)

## Editor Script

![初始化](./image/script/input.png)

- Here we demonstrate how to change the `a` declaration in a file from `let` to `const`


### Test Selector
- Click on the corresponding node to automatically copy the relevant labels

![测试选择器](./image/script/test-selector.png)

### Implementation
![实现](./image/script/replace.png)

## More?

- [Script Util](./script-util.md) Introduce