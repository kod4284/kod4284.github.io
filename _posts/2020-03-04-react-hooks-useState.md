---
layout:     post
title:      "React Hooks - useState 알아보기"
subtitle:   "React Hooks - useState"
date:       2020-03-04 20:30:00
author:     "Kod"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - React-ts
---

# React Hooks - useState 알아보기

---

### Hook이란?

v16.8 이전의 리엑트에서 Functional 컴포넌트에서는 Class 컴포넌트의 라이프 사이클 메소드 기능들을 지원하지 않아 사용할 수 없었습니다. 하지만 v16.8 버전 이후로 Hooks의 기능 도입으로 라이프 사이클 메소드들이 하는 기능들을 대체할 수 있게 되었습니다. Functional 컴포넌트에서 기존에는 할 수 없었던 상태 관리를 useState로 할 수 있게 되었고 렌더링 직후 특정 작업을 실행하게 하는 useEffect등이 도입되었습니다.

### useState

이 Hook을 사용하면 기존 Class component 에서 사용했던 state를 functional component 에서 관리 할 수 있습니다.

사용법:

```react
const [state, setState] = useState(0);
```

useState() 함수는 초기 상태 값을 인자로 받습니다. 위 코드에서는 0 이 초기 state입니다. 위 코드는 useState(0) 가 반환하는 배열을 array destructuring으로 state 변수와 setState 변수에 값들을 가져옵니다. 첫 번째 인자로는 상태(초기상태  0)을 두 번째 인자로는 상태를 설정하는 함수를 가져옵니다.

이제 간단한 counting 프로그램을 하나 만들어 보겠습니다.

React 프로젝트를 생성하는 방법은 기존 포스팅([**create-react-app Typescript 생성 및 세팅**](https://kod4284.github.io/2020/03/03/create-react-app-typescript-setting/))을 참고해주세요.

src 디렉토리에 components 디렉토리를 만들고 그 안에 Counter.tsx 컴포넌트를 생성합니다.

경로:

![디렉토리](https://kod4284.github.io/img/in-post/post-2020-03-04/counter-directory.jpg)

```react
// Counter.tsx
import React, { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);

  const onIncrease = () => {
    setCount(count + 1);
  };

  const onDecrease = () => {
    setCount(count - 1);
  };

  return (
    <div>
      <div>
        Current count:
        {count}
      </div>
      <button type="button" onClick={onIncrease}>+</button>
      <button type="button" onClick={onDecrease}>-</button>
    </div>
  )
}

export default Counter;
```

이제 Counter 컴포넌트를 최상위 컴포넌트인 App.tsx 에서 불러옵니다.

```react
// App.tsx
import React from 'react';
import Counter from './components/Counter';

function App() {
  return <Counter />;
}

export default App;
```

터미널에 ```npm start```로 확인해봅니다.

![디렉토리](https://kod4284.github.io/img/in-post/post-2020-03-04/counter.jpg)

플러스나 마이너스 버튼을 눌러 setCount 함수를 호출하면 count의 값이 바뀌게 되고 컴포넌트는 다시 렌더링 된다.