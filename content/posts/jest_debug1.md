---
title: "Fixed:jest 测试文件引入node_modules中代码时报错SyntaxError: Cannot use import statement outside a module"
date: 2024-03-10T15:33:03+08:00
draft: false
categories: ["develop"]
featuredImagePreview: "/images/jest.jpeg"
featuredImage: "/images/jest.jpeg"
---

{{< admonition type=success title="Fixed" open=false >}}
这个bug已经被解决
{{< /admonition >}}

> # 问题简述 (One-line summary)

用`jest`进行测试时，当待测试的文件引入了`node_modules`里的第三方模块，且模块是`ESM`（使用`import/export`进入导入导出）时会报错:
```shell
SyntaxError: Cannot use import statement outside a module
```
> # 问题复现 (Steps-to-reproduce)


1. 在`React`项目中编写简单的单元测试用例

```typescript
//App.test.tsx
import React from 'react';
import { render } from '@testing-library/react';
import App from '@/App';
test('renders react', () => {
	render(<App />);
	expect(1).toBe(1);
});
```

2. `App.tsx`中导入了`axios`模块

```typescript
import axios from 'axios';
```

3. `jest.config.js`配置如下,`transformIgnorePatterns`选项指定要编译`axios`模块内的内容

```javascript
module.exports = {
	preset: 'ts-jest',
	collectCoverageFrom: ['src/**/*.{js,jsx,ts,tsx}', '!src/**/*.d.ts'],
	testMatch: [
		'<rootDir>/src/**/__tests__/**/*.{js,jsx,ts,tsx}',
		'<rootDir>/src/**/*.{spec,test}.{js,jsx,ts,tsx}',
	],
	testEnvironment: 'jsdom',
	transform: {
		'^.+\\.css$': '<rootDir>/config/jest/cssTransform.js',
		'^.+\\.(js|jsx)$': 'babel-jest',
		'^.+\\.(ts|tsx)?$': 'ts-jest',
	},
	transformIgnorePatterns: ['<rootDir>/node_modules/(?!(axios))'],
	moduleNameMapper: {
		'^@/(.*)': '<rootDir>/src/$1',
	},
	watchPlugins: [
		'jest-watch-typeahead/filename',
		'jest-watch-typeahead/testname',
	],
	resetMocks: true,
	globals: {
		'ts-jest': {
			isolatedModules: true,
		},
	},
};

```

4. `.babelrc`配置如下
```json
{
	"presets": [
		["@babel/preset-env", { "targets": { "node": true } }],
		// "@babel/preset-typescript",
		"@babel/preset-react",
	],
	"plugins": ["transform-es2015-modules-commonjs"],
};

```

> # 预期效果 (What is expected)

既然已经在`jest.config.js`中通过`transformIgnorePatterns`指定了要编译`axios`模块，那么里面的`ESM`语法应该会被`babel`编译为`commonJS`语法，测试会正常运行

> # 实际效果 (What is actually happening?)

`axios`模块中的`index.js`文件报错，并且没有被编译

```shell
    Details:

    /Users/joe/Documents/Programming/react/data-resource-index/v1/node_modules/axios/index.js:2
    import axios from './lib/axios.js';
    ^^^^^^

    SyntaxError: Cannot use import statement outside a module

      1 | debugger;
    > 2 | import axios from 'axios';
        | ^
      3 | import { message } from 'antd';
      4 | const request = axios.create({
      5 |       baseURL: process.env.REACT_APP_BASE_API,

      at Runtime.createScriptFromCode (node_modules/jest-runtime/build/index.js:1728:14)

```

> # 问题原因 (Reason)

在github上查找到[issues#7578](https://github.com/jestjs/jest/issues/7578)，如果要通过`babel v7`编译`node_modules`中的模块，`babel`的配置文件应该是`babel.config.js`



> # 解决办法 (Solution)

将`.babelrc`重命名为`babel.config.js`，并将语法变成`js`语法

![solution](/images/rename_babel.png)

```javascript
//babel.config.js
module.exports = {
	presets: [
		['@babel/preset-env', { targets: { node: true } }],
		// "@babel/preset-typescript",
		'@babel/preset-react',
	],
	plugins: ['transform-es2015-modules-commonjs'],
};

```