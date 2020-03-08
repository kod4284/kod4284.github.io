---
layout:     post
title:      "create-react-app-typescript 상대경로를 절대경로로 바꾸기 v2"
subtitle:   "[version 2]CRA-typescript absolute path setting"
date:       2020-03-08 14:59:00
author:     "Kod"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - React-ts
---
# create-react-app-typescript 상대경로를 절대경로로 바꾸기 v2

---

기존에 설정하는 방법을 포스트 했는데 이전 방법에 몇 가지 문제점이 생겨서 절대 경로 세팅에 대한 두 번째 포스팅을 하게 되었습니다. [기존 포스팅](https://kod4284.github.io/2020/03/07/CRAT-setting-absolute-path/)은 @craco/craco와 craco-alias 플러그인을 사용했습니다. 하지만 craco-alias을 사용했을 때는 scss 파일을 import 할 때 **import '@styles/example.scss'** 특정 파일을 못 찾는 상황이 생겼습니다. 이번 포스팅에서는 craco-alias을 쓰지 않고 **@craco/craco** 공식 패키지만 사용해서 절대 경로 세팅을 해보겠습니다.

### 설치 방법

```shell
yarn add @craco/craco
```

### 적용하기

**package.json** 파일을 아래와 같이 수정합니다.

```js
{
  // 윗부분 생략...
  "scripts": {
    "start": "craco start",
    "build": "craco build",
    "test": "craco test",
    "eject": "react-scripts eject"
  },
  // 아랫부분 생략...
}
```

프로젝트의 루트에 **craco.config.js** 파일을 생성하고 아래와 같이 작성합니다.

```js
const path = require('path');

module.exports = {
  webpack: {
    alias: {
      '@': path.resolve(__dirname, 'src/')
    }
  },
  jest: {
    configure: {
      moduleNameMapper: {
        '^@(.*)$': '<rootDir>/src$1'
      }
    }
  }
};
```

### VSCode 가 경로를 추적하게 하기

아래의 세팅은 VSCode가 파일들을 추적할 수 있게 해줍니다. 지금 세팅으로는 VSCode가 우리가 설정한 '@'를 이해하지 못합니다. 예를 들면, 기존에는 상대 경로로 파일을 import 했을 때 Autocomplete 나 intelisence 기능이 VSCode에서 자동으로 파일들을 추적해서 보여줬었습니다. 아래의 코드는 VSCode가 '@' 와 mapping 되는 경로를 이해하게 합니다.

프로젝트의 루트에 **tsconfig.paths.json** 파일을 생성하고 아래와 같이 작성합니다.

```json
{
  "compilerOptions": {
    "baseUrl": "./",
    "paths": {
      "@/*": ["src/*"]
    }
  }
}
```

**tsconfig.json** 파일을 아래와 같이 수정합니다.

```js
{
  "extends": "./tsconfig.paths.json",
  "comilerOptions": {
    // 생략...
  },
  // 생략...
  "include": [
    "src",
    "craco.config.js"
  ],
  "exclude": [
    "node_modules",
    "**/node_modules/*"
  ]
}
```

###  Lint  설정하기

현재까지의 세팅으로도 컴파일 했을 때 잘 작동 할 것입니다. 하지만 Lint가 계속 claim을 하는 것을 볼 수 있을 텐데, EsLint에게도 '@' 가 './src'를 의미한다고 알려주는 설정을 해야 합니다.

먼저 아래의 두 패키지를 설치해 줍니다.

```shell
yarn add --dev eslint-plugin-import eslint-import-resolver-alias
```

그 다음으로는 **package.json** 파일에 **eslintConfig** 설정을 아래와 같이 합시다.

```json
 "eslintConfig": {
    "settings": {
      "import/resolver": {
        "alias": {
          "map": [
            [
              "@",
              "./src"
            ]
          ],
          "extensions": [
            ".js",
            ".tsx",
            ".css",
            ".scss"
          ]
        }
      }
    },
    "parserOptions": {
      "project": "./tsconfig.json",
    },
     // 이하 생략...
```



### EsLint 설정 분리

이렇게 위처럼 많을 설정들을 하면 package.json이 지저분해 보이는데, 루트폴더에 **.eslintrc.js** **.eslintrc.json** 등의 파일을 만들어서 eslintConfig 안의 설정을 분리해서 설정할 수 있습니다.

루트폴더에 **.eslintrc.json** 파일을 만들어서 **eslintConfig**안의 내용들을 전부 잘라내어 붙여넣고 저장해 봅시다.



### 마무리

모든 설정이 잘 끝났으면 이제 아래와 같이 import 할 수 있습니다.

```react
import React from 'react';
import Test from '@components/Test';
```

### 코드

Github:<https://github.com/kod4284/boilerplate-react-ts>

