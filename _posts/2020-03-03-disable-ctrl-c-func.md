---
layout:     post
title:      "윈도우 VSCode에서 Vim extention 사용할때 control + C 기능 끄기."
subtitle:   "VS Code 기본설정"
date:       2020-03-02 19:41:00
author:     "Kod"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - VSCode
---
# 윈도우 VSCode에서 Vim extention 사용할때 control + C 기능 끄기.

---

맥에서 VSCode 에서 Vim extention을 설치하고 개발을 하다가 윈도우로 넘어왔더니 윈도우의 복사 기능과 Vim에서의 visual mode로의 전환 기능이 control + c 로 같아서 충돌을 일으키는 현상을 마주했다.

해결법은 단순히 VSCode 에서 **setting.json** 에 몇줄 추가해주는것으로 끝이었었다.

VSCode를 연뒤 **control + shift + p**를 누르면 검색창이 하나 뜨는데 **setting.json**을 검색하고 열어보자.

아래처럼 중괄호 사이에 옵션 값을 넣어주고 저장하자.

*setting.json*
```json
{
    "vim.handleKeys": {
        "<C-c>": false,
        "<C-v>": false,
        "<C-x>": false,
        "<C-z>": false,
        "<C-f>": false,
        "<C-a>": false,
    },
}
```



위에서 대문자 C는 control 키를 의미한다.

즉 <C-c>는 control + c 조합이다.

이외의 윈도우 단축키와 충돌이 일어나는 단축키 기능을 껐다.