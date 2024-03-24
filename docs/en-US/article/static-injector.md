# I separated dependency injection from Angular:`static-injector`
- Angular's dependency injection is indeed very useful, making the dependency relationships between services more flexible and reusable
- However, its limited use within Angular restricts its effectiveness and needs to be made available on all Node/Frontend platforms.

## How to use?
- If you don't care about the implementation, you can directly [access the usage documentation](https://github.com/wszgrcy/static-injector/blob/main/readme.md)

## Why not write a package that is the same as Angular dependency injection
- A mature feature has usually undergone multiple considerations, so it is the best to not reinvent the wheel.
- Using the source code of Angular can ensure that the function is in sync with the official version, without worrying about differences between your implementation and the official version.
- Using the same logic in Node/frontend eliminates mental burden.

## Can I use the code directly?
- Of course not. First, Angular's source code is designed for its specific services, so some features that we don't need need to be removed. For example, `@Module` has dependency injection-related code, `@Host` and other component decorators, and more non-general dependencies. 
- Additionally, Angular uses dependency injection for static dependency injection, so it needs to implement its own static compilation method to ensure consistency with the official version.
- It also needs to create interfaces to call and invoke Angular's source code, ensuring the normal operation of the function.

## Is it over if it runs successfully?
- Running successfully is not the end, but the first step. The code successfully executes independently, so the next step is to ensure that the code runs in sync with the `Angular` official version, no missed new features, but also no defects are overlooked. 
- To accomplish this, a method must be found that allows stable code changes and automatically updates code to match project updates.

## Use `Code Recycle` to Stable Update and Sync Code 
- [Update synchronization script](https://github.com/wszgrcy/static-injector/tree/main/script/sync)

- Pull the Angular source code through scripts, use CSS selector syntax to query and modify code 
- Test the modified code after making changes to the code. 
- After each update, only change the tag => synchronize the update => test => adjust(if there are problems) => publish. This reduces potential issues caused by manual modifications.

## How do we know if the repository supports these features?
- [Check the examples](https://github.com/wszgrcy/static-injector/tree/main/test/fixture)
- All existing examples have been tested and verified. If you need to use other features, you can submit an issue.
