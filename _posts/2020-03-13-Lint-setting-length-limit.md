---
layout:     post
title:      "Eslint 문자열 길이 에러 설정"
subtitle:   "Eslint setting length limit error"
date:       2020-03-13 20:48:00
author:     "Kod"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - React
    - Eslint
---

# Lint 문자열 길이 에러 설정

---

아래는 한 줄당 80글자가 넘어갈 경우 lint 에러를 띄우는 설정입니다.

**package.json**파일 안의 **eslintConfig** 내부나 루트 경로의 .eslintrc.json 파일에 아래의 코드를 복사 붙여넣기 하세요.

```json
"rules": {
    "linebreak-style": 0,
    "max-len": ["error", 80, 2, {
      "ignoreUrls": true,
      "ignoreComments": false,
      "ignoreRegExpLiterals": true,
      "ignoreStrings": false,
      "ignoreTemplateLiterals": false
    }]
  }
```

이제 한 줄당 80글자가 넘어가면 lint 에러가 뜹니다.