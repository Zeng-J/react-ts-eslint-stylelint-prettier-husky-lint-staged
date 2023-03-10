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

### 安装eslint-config-airbnb-typescript

上面我们使用了`eslint`和`typescript`推荐的代码风格。
```javascript
extends: [ // 共享推荐的配置风格
  'eslint:recommended',
  'plugin:@typescript-eslint/recommended',
],
```
但是受经常使用antd库的影响，习惯了[airbnb](https://github.com/airbnb/javascript)代码风格，而且比较流行。因此我们安装下`eslint-config-airbnb-typescript`（不喜欢可以忽略这一步）。

安装前我们需要先了解
- `eslint-config-airbnb`是`Airbnb JavaScript`风格的eslint共享配置库，检测规则包括`ES6+` 和 `React`，它依赖于`eslint-plugin-import`、`eslint-plugin-react`、`eslint-plugin-react-hooks`、`eslint-plugin-jsx-a11y`包。
- `eslint-config-airbnb-base`，如果我们不需要`React`，可以安装这个包
- `eslint-config-airbnb-typescript`，支持typescript，依赖于`eslint-config-airbnb`

现在动手

我们先执行`npm info "eslint-config-airbnb@latest" peerDependencies`，了解`eslint-config-airbnb`的依赖包版本

```shell
npm info "eslint-config-airbnb@latest" peerDependencies

{
  eslint: '^7.32.0 || ^8.2.0',
  'eslint-plugin-import': '^2.25.3',
  'eslint-plugin-jsx-a11y': '^6.5.1',
  'eslint-plugin-react': '^7.28.0',
  'eslint-plugin-react-hooks': '^4.3.0'
}
```
知道版本后，我们安装对应的版本
```shell
yarn add --dev eslint-plugin-import@^2.25.3 eslint-plugin-jsx-a11y@^6.5.1 eslint-plugin-react@^7.28.0 eslint-plugin-react-hooks@^4.3.0
```

接着安装`eslint-config-airbnb`和`eslint-config-airbnb-typescript`
```shell
yarn add --dev eslint-config-airbnb eslint-config-airbnb-typescript
```

按照[eslint-config-airbnb-typescript配置步骤](https://github.com/iamturns/eslint-config-airbnb-typescript#3-configure-eslint), 现在重新调整`.eslintrc.js`文件
```javascript
module.exports = {
  root: true,
  env: {
    browser: true,
    node: true,
    es6: true
  },
  extends: [
    'airbnb',
    'airbnb-typescript',
    'airbnb/hooks',
    'plugin:@typescript-eslint/recommended',
  ],
  parser: '@typescript-eslint/parser',
  plugins: ['@typescript-eslint'],
  parserOptions: {
    ecmaVersion: "latest",
    sourceType: "module",
    ecmaFeatures: {
      jsx: true
    },
    project: './tsconfig.json'
  },
  rule: {
    "react/react-in-jsx-scope": "off",
  }
}

```

至此，我们可以在`package.json`添加命令
```json
{
  "script": {
    "lint:js": "eslint --ext .js,.jsx,.ts,.tsx ./src"
  }
}
```
执行`yarn lint:js`检测我们的代码