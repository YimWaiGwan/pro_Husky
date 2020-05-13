# Husky
1. 安装相关的包(husky,lint-staged,@commitlint/cil,@commitlint/config-conventional)
lint-staged：用户实现每次提交只检查提交本次所修改的文件
```js
npm i -D husky lint-staged @commitlint/cli @commitlint/config-conventional
```
> 注意：一定要使用npm安装eslint和husky，因为在windows操作系统下，用yarn安装依赖，不会触发husky pre-commit钩子命令

2. 在项目根目录下创建.huskyrc
```json
{
  "hooks": {
    "pre-commit": "lint-staged",
    "commit-msg": "commitlint -E HUSKY_GIT_PARAMS"
  }
}
```
3.在项目根目录下创建.lintstagedrc
```js
{
  "src/**/*.js": "eslint"
}
```
4. 创建comitlint.config.js
```js
module.exports = {
  extends: ['@commitlint/config-conventional'],
  rules: {
    'type-enum': [
        2,
        'always',
        ['feat', 'fix','docs', 'style','refactor', 'test', 'revert','config','chore'],
    ],
    'subject-full-stop': [0, 'never'],
    'subject-case': [0, 'never'],
  }
}
```
用于说明commit的类别，只允许使用下面的7个标识
* feat：新功能(feature)
* fix：修补bug
* docs：文档(documentation)
* style：格式(不影响代码运行的变动)
* refectory：重构
* test：增加测试
* chore：构建过程或辅助工具的变动
> 注：提交信息必须是规定的7个标识开始。并跟随一个英文的冒号和一个空格，接着是提交的内容