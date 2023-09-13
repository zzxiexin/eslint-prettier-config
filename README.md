## 保姆级Eslint && Prettier && Git hooks && VScode配置

#### 一、Eslint 安装 && 配置

1、安装 eslint

```javascript
pnpm add eslint -D
```

2、执行初始化配置命令,生成.eslintrc.js 文件

```javascript
pnpm eslint --init
```

3、按照自己项目配置选择合适配置   

<img width="1000" alt="image" src="https://github.com/zzxiexin/eslint-prettier-config/assets/24984301/b39cc105-21b5-4e29-a390-fd93f3f9b78f">


4、新增脚本命令

```javascript
"lint": "eslint . --ext .vue,.js,.ts,.jsx,.tsx --fix"
```

5、vscode安装ESLint插件  

6、安装 vscode 插件 ESLint（保存代码自动格式化，跟项目走的配置）
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

#### 二、Prettier 安装 && 配置

1、安装 Prettier

```javascript
pnpm add prettier -D
```

2、新增 .prettierrc.js 文件

3、在线格式化规则设置，在线配置合适的配置文件，并以 cjs 输出到.prettierrc.js 文件中
https://www.prettier.cn/playground   


4、新增脚本命令

```javascript
 "format": "prettier --write src/"
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

#### 如何解决 Eslint 和 Prettier 校验代码风格冲突 ？？？

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

#### 三、Git hooks 配置（git提交强制校验）

1、安装 pnpm add husky lint-staged -D

```javascript
pnpm add husky -D
```

2、运行

```javascript
pnpm husky install || npx husky install
```

3、添加 commit 钩子

```javascript
pnpm husky add .husky/pre-commit "pnpm lint && pnpm format"
```

#### 编辑器设置(如果项目没有设置.vscode/settings.json，则可以配置全局的 vscode)

1、安裝插件 Prettier - Code formatter  
2、Vscode -》 首选项 -》 设置（搜索 save）-》 勾选 Editor: Format On Save 即可

### 相关问题及姿势
1、Q：eslint extends 配置 prettier  
A：https://github.com/prettier/eslint-config-prettier#installation  
   
2、Q：'React' must be in scope when using JSX react/react-in-jsx-scope?  
A: https://stackoverflow.com/questions/42640636/react-must-be-in-scope-when-using-jsx-react-react-in-jsx-scope  
   
3、Q：eslint-plugin-react 报未指定 react 版本的 Warning: React version not specified in eslint-plugin-react settings.  
A：https://blog.csdn.net/keepfriend/article/details/100858645  
   
4、Q：.eslintrc.js module is not defined  
A：https://www.anycodings.com/questions/eslintrcjs-module-is-not-defined   
   
5、Q: extends和plugins有什么区别   
A：plugins是插件预设好的一些新的规则，默认会开启内部部分规则和关闭一些规则，可以按照自己需要去开启或者关闭,在rules去配置，extends则是复用别人的规则;  
   
6、Q: extens执行顺序是怎么样的？   
A: 是从左往右的；   
   
7、eslint或者prettier都可以封装一个自己的npm配置包，作为公用；
Prettier config plugin:
<img width="832" alt="image" src="https://user-images.githubusercontent.com/24984301/195373680-95aa882f-bb92-4159-ab0f-c92dfbcf0b58.png">
<img width="791" alt="image" src="https://user-images.githubusercontent.com/24984301/195375749-d9b4833b-3c4a-4564-ba54-5f73bdf8d144.png">

Eslint config plugin:
<img width="885" alt="image" src="https://user-images.githubusercontent.com/24984301/195373997-4bc87eb3-efdd-4896-a701-1c91f51285b0.png">
<img width="1168" alt="image" src="https://user-images.githubusercontent.com/24984301/195375522-778be418-d7db-4294-8f61-b9d1e1697aa7.png">
8、处理打开.eslintrc.js 处理报错  
Q: module is not defined  
A1: .eslintrc,js 属性 env 新增 node: true  
A2: .eslintrc.js 更改为.eslintrc.cjs

9、 error 'React' must be in scope when using JSX react/react-in-jsx-scope;  
A: .eslintrc.js 属性 rules 新增"react/react-in-jsx-scope": "off"

10: React version not specified in eslint-plugin-react settings.  
A: .eslintrc.js 新增

```javascript
  settings: {
    react: {
      version: 'detect',
    },
  },
```
11、相关姿势   
1.  为什么项目装了vscode还需要装eslint？
 因为项目装的是npm包，每次提交代码或者运行命令才能检查错误，不能做到实时，而vscode的eslint插件可以提供实时错误检查和提示、自动修复功能、代码提示和建议等功能   
 
1.  eslint是只可以校验js代码吗？
ESLint 最初是为校验 JavaScript 代码而创建的，它提供了一套强大的规则和插件来检查 JavaScript 文件的语法、代码风格和潜在问题。但是，随着时间的推移，ESLint 已经发展成为一个灵活的工具，可以用于校验多种类型的文件。
除了 JavaScript 文件，ESLint 也支持校验其他类型的文件，包括：
TypeScript：通过使用 @typescript-eslint/parser 解析器和 @typescript-eslint/eslint-plugin 插件，可以对 TypeScript 文件进行静态代码分析。
Vue：通过使用 eslint-plugin-vue 插件，可以对 Vue.js 单文件组件进行校验。
JSX/React：通过使用 eslint-plugin-react 插件，可以对 JSX 和 React 代码进行校验。
HTML：通过使用 eslint-plugin-html 插件，可以对嵌入 JavaScript 代码的 HTML 文件进行校验。
通过配置不同的解析器和插件，你可以扩展 ESLint 的功能，使其能够校验更多类型的文件。你可以根据项目需求安装相应的解析器和插件，并在配置文件中进行相应的设置。

需要注意的是，虽然 ESLint 可以校验多种类型的文件，但它在校验非 JavaScript 文件时可能会有一些限制，例如无法识别特定类型的语法或规则。在使用 ESLint 进行跨文件类型的校验时，建议查阅相关的文档和配置指南，以确保正确配置插件和规则。


