# hybridize the project?You can initialize it at any location in the Git Repo as a template combination.
- Currently, when we initialize a project, we might use the Use this template in Github, or directly pull a repository.
- But it is more of an instance stored in a folder within the repository. Developers will not build a separate repository for a template, so at this time, we need to fetch the entire repository, then extract the corresponding file.

## Using sparse to fetch.
- Of course, Git can also support fetching only certain folders, but would you really want to manually type this complicated command every time?

```shell
git clone --filter=blob:none --no-checkout --sparse xxxx --depth 1 --branch yyyy ./zzz
cd ./zzz
git sparse-checkout set foo
git checkout yyyy
```

## Git repository pull in `Code Recycle`.

![](https://cdn.jsdelivr.net/gh/wszgrcy/code-recycle@1.1.3/docs/en-US/image/git-template-demo.png)

- `Code Recycle` is currently a VS Code extension that [supports pulling Git repositories](https://wszgrcy.github.io/code-recycle/#/en-US/design/custom-rule?id=git-template)
- Any content can be pulled at any location and written to any location.
- You can pull multiple repositories at one time and place them in the specified location.
> Your initial project may not necessarily come from one repository.
- If you find it troublesome, you can directly modify the above resource `git-template-demo`, and the resources are already placed in the [public area](https://wszgrcy.github.io/code-recycle/#/en-US/public?id=add-public-resources). You can directly copy and modify the pull request link to use it.
> Or you can directly modify the input parameters as [interactive retrieve](https://wszgrcy.github.io/code-recycle/#/en-US/design/custom-rule?id=action-global-variables) or [visual operation](https://wszgrcy.github.io/code-recycle/#/en-US/design/custom-rule?id=visual-action), the `Code Recycle` library provides a rich range of code modification operations to meet the needs of most scenarios.


### Quick start
- If you are already thinking about it, you might as well take a [look at the documentation](https://wszgrcy.github.io/code-recycle/#/en-US/README) to see how to use it.
