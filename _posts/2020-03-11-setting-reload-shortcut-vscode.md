---
layout:     post
title:      "VSCode 재시작 단축키 설정"
subtitle:   "Setting a shortcut to reload VSCode"
date:       2020-03-11 20:48:00
author:     "Kod"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - VSCode
---

# VSCode 재시작 단축키 설정

---

여러 작업들을 하다 보면 VSCode의 작동이 이상할 때가 있습니다. 예를 들면 린트 에러가 지워져야 하는데 계속 남아있는 증상들이 있습니다. 그때마다 항상 VSCode를 껐다가 키면 증상은 사라지지만 귀찮은 작업입니다. 이를 단축키 하나에 바인딩 하여 VSCode를 리로딩 하는 방법을 알아보겠습니다.

**F1** 이나 **ctrl + shift + p**를 입력하고 **Open keyboard shortcuts (JSON)** 에 들어갑니다.

아래의 코드를 복사 붙여넣기 하고 저장합니다.

```json
[
  {
    "key": "ctrl+f5",
    "command": "workbench.action.reloadWindow",
    "when": "editorTextFocus"
  }
]
```

이제 VSCode에서 **ctrl + f5**를 눌러보면 리로딩 됩니다!