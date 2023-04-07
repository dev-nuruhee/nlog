---
title: React - Class Component VS Functional Component
published: true
---

뭐 요즘은 잘안쓴다고 하긴 하는데 그래도 개발자들은 언젠가 사용할 일이 있다..
그리고 왜 안쓰는지에 대해 젱리 쉽게 아는 방법은 실제 써봐야지.

일단 Vite로 구성해뒀던 React Project에 테스트를 해보자!

**test.jsx**
``` javascript
import React from "react";
function test(){
    return (
        <div>test입니다 </div>
    );
}
export default test;
```

**testcase.jsx**
``` javascript
import React from "react";
function Testcase(){
    return (
        <div>Test.jsx입니다! </div>
    );
}
export default Testcase;
```

이 두 개의 jsx파일을 구성하고 main.jsx에 붙여보자

```javascript
import React from 'react'
import ReactDOM from 'react-dom/client'
import App from './App'
import Test from './Test'
import Testcase from './Testcase'
import './index.css'

ReactDOM.createRoot(document.getElementById('root')).render(
  <React.StrictMode>
    ==================================
    <App />
    ==================================
    <TestFunc />
    <TestClass />
  </React.StrictMode>
)

```
![image](https://user-images.githubusercontent.com/88364980/230306858-a7864f24-806b-495e-9a02-1c6b8a985af4.png)


이런 코드들을 클래스 컴포넌트들을 바꿔보자!

```javascript
/*function component*/
import React from "react";

function TestFunc(){
    return (
        <div>TestFunc입니다</div>
    );
}

export default TestFunc;
```

```javascript
/*class component*/
import React, { Component } from "react";

class TestClass extends Component{
    render () {
        return (
            <div>TestClass입니다</div>
        );
    }
}

export default TestClass;
```
 

클래스 컴포넌트에서는 function 이 class로 바꾸고 Component를 상속 받는다.
또한 클래스 컴포넌트에서는 render()를 사용한다.

자 문법이 다른걸 알겠으나, 실제 동작하는데 어떤 차이가 있나 보자.

클릭하면 숫자가 증가하는 버튼을 만들어보자.
```javascript
/*function component*/
import React, { useState } from "react";
function TestFunc(){
    const [ count, setCount ] = useState(0);
    function countIncrease() {
        const newCount = count+1;
        setCount(newCount);
    }
    return (
        <>
            <div>TestFunc입니다</div>
            <button onClick={countIncrease}>function Increase! {count} </button>
        </>
    );
    
}

export default TestFunc;
```

```javascript
/*class component*/
import React, { Component } from "react";

class TestClass extends Component{
    state = {
        count : 0,
    };
    countIncrease = () => {
        const newCount = this.state.count + 1;
        this.setState( { count: newCount });
    }
    render () {
        return (
            <>  
                <div>TestClass입니다</div>
                <button onClick={this.countIncrease}>class Increase! {this.state.count} </button>
            </>
        );
    }
}

export default TestClass;
```


차이를 분석해보자.
1. 클래스 컴포넌트 사용시엔 코드가 늘어난다.
2. 클래스 컴포넌트에선 라이프 사이클과 state관리가 코드에서 직접 이루어짐.
3. 함수형 컴포넌트에선 라이프 사이클과 state관리를 hook에서 한다.



