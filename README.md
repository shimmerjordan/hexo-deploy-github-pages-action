> 相较于原作者的版本，这里参考 https://github.com/blinkfox/hexo-theme-matery/issues/119 修复了mathjax在hexo中无法正确渲染多行公式的问题：
> ```shell
> echo ">_ 覆盖node_modules中需要修改覆盖的文件 ..."
> \cp backup/inline.js node_modules/kramed/lib/rules/inline.js
> ```
> 脚本中在`npm install`之后新增了这些

# Hexo Deploy GitHub Pages Action

This GitHub action for building and deploying Hexo project to GitHub pages.

## Getting Started

You can view an example of this below.

```yml
name: Hexo Deploy GitHub Pages
on:
  push:
    branches:
      - master
jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    
    steps:
    - name: Checkout
      uses: actions/checkout@v3
      with:
        fetch-depth: 0

    - name: Build and Deploy
      uses: theme-keep/hexo-deploy-github-pages-action@master
      env:
        # Your GitHub Token
        PERSONAL_TOKEN: ${{ secrets.GITHUB_TOKEN }}

        # The repository the action should deploy to
        PUBLISH_REPOSITORY: theme-keep/site
```

## Configuration item

The `env` portion of the workflow **must** be configured before the action will work. You can add these in the `env` section found in the examples above. Any `secrets` must be referenced using the bracket syntax and stored in the GitHub repositories `Settings / Secrets and variables / Actions` menu. You can learn more about setting environment variables with GitHub actions [here](https://help.github.com/en/articles/workflow-syntax-for-github-actions#jobsjob_idstepsenv).

Below you'll find a description of what each option does.

| Key                  | Value Information                                                                                                                                                                                                                                                                                                     | Type | Default | Required |
|----------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------| ------------- |---------| ------------- |
| `PERSONAL_TOKEN`     | Depending on the repository permissions you need to provide the action with a GitHub Personal Access Token in order to deploy. You can [learn more about how to generate one here](https://help.github.com/en/articles/creating-a-personal-access-token-for-the-command-line). **This should be stored as a secret**. | `secrets` |         | **Yes** |
| `PUBLISH_REPOSITORY` | The repository the action should deploy to. for example `theme-keep/site`                                                                                                                                                                                                                                             | `env` |         | **Yes** |
| `BRANCH`             | The branch the action should deploy to. for example `master`                                                                                                                                                                                                                                                          | `env` | `gh-pages` | No |
| `PUBLISH_DIR`        | The folder the action should deploy. for example `./public`                                                                                                                                                                                                                                                           | `env` | `./public` | No |
| `CNAME` | The domain name of your GitHub Page specified in a CNAME                                                                                                                                                                                                                                                              | `env` |  | No |
