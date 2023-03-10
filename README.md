## 安装eslint
安装执行`yarn add --dev eslint`

项目目录添加`.eslintrc.js`
```javascript
module.exports = {
  root: true, // 指定了root为true，eslint只检查当前项目目录
  env: { // 提供预设的全局变量，避免eslint检查报错，例如window
    browser: true,
    node: true,
    es6: true
  },
  extends: [ // 继承eslint推荐的检查规则
    'eslint:recommended'
  ],
  parserOptions: {
    ecmaVersion: "latest", // 指定ECMAScript 语法为最新
    sourceType: "module", // 指定代码为 ECMAScript 模块
    ecmaFeatures: {
      jsx: true // 启用jsx
    }
  },
}
```

项目目录添加`.eslintignore`
```
.eslintrc.js
node_modules
dist
.DS_Store
*.local
```

### 安装typescript-eslint

由于我们项目使用的是`Typescript`，所以得改下eslint解释器，参考[typescript-eslint](https://typescript-eslint.io/getting-started)

安装执行`yarn add --dev @typescript-eslint/parser @typescript-eslint/eslint-plugin`

改变`.eslintrc.js`
```javascript
module.exports = {
  root: true, // 指定了root为true，eslint只检查当前项目目录
  env: { // 提供预设的全局变量，避免eslint检查报错，例如window
    browser: true,
    node: true,
    es6: true
  },
  extends: [ // 共享推荐的配置风格
    'eslint:recommended',
    'plugin:@typescript-eslint/recommended',
  ],
  parser: '@typescript-eslint/parser',
  plugins: ['@typescript-eslint'],
  parserOptions: {
    ecmaVersion: "latest", // 指定ECMAScript 语法为最新
    sourceType: "module", // 指定代码为 ECMAScript 模块
    ecmaFeatures: {
      jsx: true // 启用jsx
    }
  },
}
```