### 项目配置 Eslint && Prettier && Git hooks && VScode

#### Eslint 安装&&配置

1、安装 eslint

```javascript
pnpm add eslint -D
```

2、执行初始化配置命令,生成.eslintrc.js 文件

```javascript
pnpm eslint --init
```

3、新增脚本命令

```javascript
"lint": "eslint . --ext .vue,.js,.ts,.jsx,.tsx --fix"
```

4、处理打开.eslintrc.js 处理报错  
Q: module is not defined  
A1: .eslintrc,js 属性 env 新增 node: true  
A2: .eslintrc.js 更改为.eslintrc.cjs

Q: error 'React' must be in scope when using JSX react/react-in-jsx-scope;  
A: .eslintrc.js 属性 rules 新增"react/react-in-jsx-scope": "off"

Q: React version not specified in eslint-plugin-react settings.  
A: .eslintrc.js 新增

```javascript
  settings: {
    react: {
      version: 'detect',
    },
  },
```

5、安装 vscode 插件 ESLint（保存代码自动格式化，跟项目走的配置）
在项目中新建.vscode/settings.json 文件，然后在其中加入以下配置；

```javascript
{
    // 开启自动修复
    "editor.codeActionsOnSave": {
        "source.fixAll": false,
        "source.fixAll.eslint": true
    }
}
```

#### Prettier 安装 && 配置

1、安装 Prettier

```javascript
pnpm add prettier -D
```

2、新增 .prettierrc.js 文件

3、在线格式化规则设置，在线配置合适的配置文件，并以 cjs 输出到.prettierrc.js 文件中
https://www.prettier.cn/playground

4、新增脚本命令

```javascript
"format": "prettier --write \"./**/*.{html,vue,ts,js,json,md}\"
```

5、安装 vscode 插件 Prettier - Code formatter

6、在.vscode/settings.json 中添加一下规则（跟项目走的配置）

```javascript
{
    // 保存的时候自动格式化
    "editor.formatOnSave": true,
    // 默认格式化工具选择prettier
    "editor.defaultFormatter": "esbenp.prettier-vscode"
}
```

### 解决 Eslint 和 Prettier 冲突

> 在理想的状态下，eslint 与 prettier 应该各司其职。eslint 负责我们的代码质量，prettier 负责我们的代码格式。但是在使用的过程中会发现，由于我们开启了自动化的 eslint 修复与自动化的根据 prettier 来格式化代码。所以我们已保存代码，会出现屏幕闪一起后又恢复到了报错的状态。
> 这其中的根本原因就是 eslint 有部分规则与 prettier 冲突了，所以保存的时候显示运行了 eslint 的修复命令，然后再运行 prettier 格式化，所以就会出现屏幕闪一下然后又恢复到报错的现象。这时候你可以检查一下是否存在冲突的规则。
> 查阅资料会发现，社区已经为我们提供了一个非常成熟的方案，即 eslint-config-prettier + eslint-plugin-prettier。
> eslint-plugin-prettier： 基于 prettier 代码风格的 eslint 规则，即 eslint 使用 pretter 规则来格式化代码。
> eslint-config-prettier： 禁用所有与格式相关的 eslint 规则，解决 prettier 与 eslint 规则冲突，确保将其放在 extends 队列最后，这样它将覆盖其他配置

```javascript
pnpm add eslint-config-prettier eslint-plugin-prettier -D
```

.eslintrc.js 属性 extends 新增

```javascript
'plugin:prettier/recommended';
```

完整的.eslintrc.js 配置代码如下：

```javascript
module.exports = {
  env: {
    browser: true,
    es2021: true,
    node: true,
  },
  extends: ['eslint:recommended', 'plugin:react/recommended', 'plugin:prettier/recommended'],
  overrides: [],
  parserOptions: {
    ecmaVersion: 'latest',
    sourceType: 'module',
  },
  plugins: ['react'],
  rules: {
    'react/react-in-jsx-scope': 'off',
  },
  settings: {
    react: {
      version: 'detect',
    },
  },
};
```

#### Git hooks 配置

1、安装 pnpm add husky lint-staged -D

```javascript
pnpm add husky -D
```

2、设置脚本命令

```javascript
"prepare": "husky install"
```

3、运行

```javascript
pnpm prepare
```

4、添加 commit 钩子

```javascript
pnpm husky add .husky/pre-commit "pnpm lint && pnpm format"
```

#### 编辑器设置(如果项目没有设置.vscode/settings.json，则可以配置全局的 vscode)

1、安裝插件 Prettier - Code formatter  
2、Vscode -》 首选项 -》 设置（搜索 save）-》 勾选 Editor: Format On Save 即可

### 遇到的问题

1、A：eslint extends 配置 prettier  
Q：https://github.com/prettier/eslint-config-prettier#installation  
2、A：'React' must be in scope when using JSX react/react-in-jsx-scope?  
Q: https://stackoverflow.com/questions/42640636/react-must-be-in-scope-when-using-jsx-react-react-in-jsx-scope  
3、A：eslint-plugin-react 报未指定 react 版本的 Warning: React version not specified in eslint-plugin-react settings.  
Q：https://blog.csdn.net/keepfriend/article/details/100858645  
4、Q：.eslintrc.js module is not defined  
A：https://www.anycodings.com/questions/eslintrcjs-module-is-not-defined
