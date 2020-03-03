---
layout:     post
title:      "create-react-app Typescript 생성 및 기본세팅."
subtitle:   "CRA-typescript basic settings"
date:       2020-03-03 20:11:00
author:     "Kod"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - React-ts
---

# create-react-app Typescript 생성 및 세팅

---

create-react-app-typescript 프로젝트를 생성하고 기본적으로 해야할 세팅을 적어보았다.

### Extension  설치

React로 개발할때 생산성을 높여주는 VSCode extension 리스트인데 취향대로 설치하면 된다. 

* Prettier
* Gitblame
* ESLint
* Vim(optional)

### setting.json

*VSCode에서* Tab을 눌렀을 때 기본적으로 4칸이 띄어질 텐데, 보통은 double space로 설정한다. **Crtl + Shift + P** 입력 후 **setting.json** 안에 아래 코드를 붙여 넣자.

* 탭 사이즈 double space로 만들기

  ```json
  {
      "editor.tabSize": 2,
      "editor.insertSpaces": true,
  }
  ```

### create-react-app 생성

CRA-typescript 프로젝트를 생성해보자.  yarn을 사용한다면 npx로 시작하는 줄 아래 것을 터미널에서 실행하면 된다.

```sh
npx create-react-app my-app --template typescript

# or

yarn create react-app my-app --template typescript
```

### eslint 설정

eslint는 React 앱 개발할 때 거의 필수적으로 쓰인다. 그 이유는 자바스크립트가 컴파일 언어가 아니기 때문에 컴파일 타임에 에러를 잡아주지 못하기 때문이기도 하다. eslint가 제시하는 대로 코드를 작성하면 많은 실수와 에러를 run 하지 않아도 잡을 수 있다. 많은 eslint configuration 이 있지만 가장 유명하고 많이 쓰이는 Airbnb에서 만든 것을 사용하겠다.

프로젝트의 디렉토리에서 아래의 코드를 실행해서 설치하자.

```shell
# Using npm
npm install eslint-config-airbnb-typescript \
            eslint-plugin-import@^2.18.2 \
            eslint-plugin-jsx-a11y@^6.2.3 \
            eslint-plugin-react@^7.15.1 \
            eslint-plugin-react-hooks@^1.7.0 \
            @typescript-eslint/eslint-plugin@^2.19.0 \
            --save-dev
# Using yarn
yarn add eslint-config-airbnb-typescript \
         eslint-plugin-import@^2.18.2 \
         eslint-plugin-jsx-a11y@^6.2.3 \
         eslint-plugin-react@^7.15.1 \
         eslint-plugin-react-hooks@^1.7.0 \
         @typescript-eslint/eslint-plugin@^2.19.0 \
         -D
```

마지막으로 package.json 안에 있는 eslintConfig 안에 아래처럼 작성하면 eslint 가 적용된다.

```shell
# eslint configuration in package.json
"eslintConfig": {
   "extends": ["airbnb-typescript"],
   "parserOptions": {
   "project": "./tsconfig.json"
   }
   "rules": { # 윈도우에서 개행문자가 \n이 아니라 \r\n 인 것 때문에 에러막기 위한 옵션 
      "linebreak-style": 0
   }
},
```

