---
layout:     post
title:      "React Typescript "Could not find a declaration file for module" 오류 해결하기"
subtitle:   "React-ts "Could not find a declaration file for module" error handling"
date:       2020-03-10 23:07:00
author:     "Kod"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - React-ts
---

# React Typescript "Could not find a declaration file for module" 오류 해결하기

---

`yarn add classnames`로 classnames 모듈을 설치했는데 VSCode에서 **"Could not find a declaration file for module"** 이라는 에러를 내뿜었습니다.

타입스크립트를 쓰지 않았을때는 보지 못했던 오류라 당황했지만 알아본결과 타입스크립트는 외부 모듈을 설치하고나서도 따로 그 모듈을 불러오는 인터페이스가 필요하다고 합니다.

VSCode에서 claiming 하는 메세지대로 `npm install @types/classnames`로 특정모듈을 설치했더니 해결되었습니다. `npm install @types/<module name>`하면 될 듯 합니다.