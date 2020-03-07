---
layout:     post
title:      "create-react-app-typescript 상대경로를 절대경로로 바꾸기"
subtitle:   "CRA-typescript absolute path setting"
date:       2020-03-07 16:24:00
author:     "Kod"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - React-ts
---
# create-react-app-typescript 상대경로를 절대경로로 바꾸기

---

CRA의 기본 세팅으로 앱을 개발하다 보면 폴더 구조가 점점 복잡해지거나 깊어질 수 있는데, 이럴 때 기본 세팅인 상대 경로로 import를 하다 보면 가독성이 떨어질 수밖에 없습니다. 이러한 문제는 절대 경로로 import 할 수 있게 세팅을 바꿔주면 해결할 수 있습니다. 하지만 CRA는 webpack 설정이 숨겨져 있고 이를 수정하려면 프로젝트를 eject 해야 하는데, 한번 eject 하면 다시는 되돌릴 수 없고 많은 설정 파일들이 그대로 노출되기 때문에 가독성이 떨어집니다. 또한 Facebook 측에서 CRA를 업데이트했을 때 그 업데이트를 받아오면서 설정들이 자동으로 변경되어 적용되는 장점을 잃게 되어 버립니다.

이것은 **craco** 라는 라이브러리를 적용하면 프로젝트를 eject 하지 않고도 설정을 바꿀 수 있습니다.

### 설치 방법

```shell
yarn add @craco/craco
yarn add --dev craco-alias
```

### 적용하기

**package.json** 파일을 아래와 같이 수정합니다.

```json
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

프로젝트의 루트에 **tsconfig.paths.json** 파일을 생성하고 아래와 같이 작성합니다.

```json
{
	"compilerOptions": {
		"baseUrl": "./src",
		"paths": {
			"@components/*": [
                "./components/*"
            ]
            // 에러문제로 주석은 꼭 지워주세요!
            // "<쓰고싶은alias/*>" : ["<baseUrl의 값 기준 경로 ex) ./ 는 src를 의미>"]
		}
	}
}
```

프로젝트의 루트에 **craco.config.js** 파일을 생성하고 아래와 같이 작성합니다.

```json
const CracoAlias = require('craco-alias');

module.exports = {
	plugins: [
		{
			plugin: CracoAlias,
			options: {
				source: 'tsconfig',
 				baseUrl: './src', // tsconfig.paths.json에 있는 baseUrl 경로값과 맞춰줍니다.
				tsConfigPath: 'tsconfig.paths.json',
                debug: false // 에러가 날 경우 true로 바꾸고 디버깅 하면 대부분의의 문제해결!
			},
		},
	],
};
```

마지막으로 **tsconfig.json** 파일을 아래와 같이 수정합니다.

```json
{
    "extends": "./tsconfig.paths.json",
    "comilerOptions"{
    	// 생략...
	}
	// 생략...
}
```

모든 설정이 잘 끝났으면 이제 아래와 같이 import 할 수 있습니다.

```react
import React from 'react';
import Test from '@components/Test';
```

