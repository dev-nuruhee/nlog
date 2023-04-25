---
title: React - React Router & State Management
published: true
---
### React Router ###
Router는 기본적으로 URL을 변경하고 URL에 맞는 페이지를 보여주는 것이라고 생각하면 된다.
여기서 SPA에 대한 이해가 필요하다.
SPA같은 경우 최초 로딩시에 모든 요소들을 로드해오는데 조건에 맞는 요소들만 보여주는 것이다.
그렇기 때문에 최초 로딩시에 조금 느릴 수 있으나 로딩 후에는 엄청나게 빠른 반응 속도를 보여주는 것이다.

사용하는 방법은?
```cmd
npm install react-router-dom   /*react-router-dom 설치*/
```

```javascript
import {
  BrowserRouter as Router,
  Routes,
  Route
} from "react-router-dom";
/*설치한 react-router-dom import하고 그 중 BrowserRouter를 Router라고 약칭*/
/*여러 Route를 할당하기 위한 Routes 정의*/
/*Route를 이동할 각 페이지들의 주소를 할당*/


ReactDOM.createRoot(document.getElementById('root') as HTMLElement).render(
  <React.StrictMode>
    <Router>
     <Routes>
       <Route path="/" element={<RealMain/>}/>
       <Route path="/FirstDepth/*" element={<FirstDepth />}/>
       <Route path="/SecondDepth/*" element={<SecondDepth />}/>
       <Route path="/ThirdDepth/*" element={<ThirdDepth />}/>
       <Route path="/ViewResult/*" element={<ViewResult />}/>
     </Routes>
    </Router>
  </React.StrictMode>,
)
```

위와 같이 설정해놓으면
http://localhost:port/
http://localhost:port/FirstDepth
http://localhost:port/SecondDepth
http://localhost:port/ThirdDepth
http://localhost:port/ViewResult

각 컴포넌트들이 페이지 주소를 갖는 것이다.
어떤 이벤트가 발생했을 때 해당 주소로 보내는 기능이 하나 더 있다.
그건 바로 Link 이다.
주소를 만들었으면 해당 주소로 이동을 해야할 것이 아닌가?
클라이언트 입장에서는 주소를 다 외우거나 확인할 수는 없으니.. 

```javscript
import {Link} from "react-router-dom";
function RealMain() {
  return (
    <>
        <TopTitle titleValue="당신만의 소설을 만들어보세요!"></TopTitle>
        <Mainlogo></Mainlogo>
        <Link to="/FirstDepth">
            <Button children="시작하기!" ></Button>
        </Link>
        <ShareIcon/>
    </>
  )
}
export default RealMain
```

위 처럼 사용하면 된다!

### State Management ###

State를 관리하는 여러가지 라이브러리들이 있다.
사용 동향을 확인해보면 redux가 압도적으로 많다.
https://fe-tool.com/awesome-react-state-management
가장 많이 사용하는 react state library인 react redux에 대해 알아보자.

### react redux ###
useState를 사용할 경우 컴포넌트 내부에서 state를 만들고 함수를 통해 바꾼다.
하지만 redux는 컴포넌트에 종속되지 않고 컴포넌트 바깥에서 가능하다.
redux는
**Action -> Dispatch > Store -> View**인 **flux 패턴**을 따른다.
어떤 **Action**이 발생하면 **Dispatcher**가 state를 변경한 후에 **Store**에 저장하고 **View**로 보여준다. 

설치
```cmd
npm install --save react-redux
```

redux를 사용하기 이전에 중요사항이 있다.
불변성을 유지해주어야 한다.
이 불변성에 대해서 좀 알아봐야 하는데..

```javascript
const obj1 ={}
const obj2 ={}

obj1 === obj2 //false
```

react는 항상 이 문제에 대해서 다루곤 하는데 두 객체는 각각 고유성을 가지고 있다.
리턴하는 값이 같더라도 실제로는 다른 객체라는 것이다.

```javascript
const obj1 = {a:2};
const obj2 = obj1.a

obj2 === obj1.a // true
```
이 것을 보면 두 객체는 또 같다.
왜냐면 참조 관계가 되기 때문이다.

객체 자체는 다르나 참조하는 값은 같다는 것이다.
그런데 이게 불변성이랑 무슨 관련이 있냐고 한다면 우리는 리듀서에 대해서 모르기 때문에 하는 말이다.
리듀서는 이전 State와 Action 객체를 파라미터로 받는다.
이전 State 절대로 건드리지 않고, 참조되는 값이 바뀐 새로운 State 객체를 만들어서 반환한다.
결국 무슨 말이냐? State의 참조값을 바꾼다고 한들 새로운 객체의 참조값을 반환하는 것이고
항상 같은 인자를 가진 Redux는 같은 결과값을 리턴한다는 것이다.
다른 결과값을 리턴하기 위해선 다른 인자를 넣어야 된다는거다.

** redux 작성 방법 **
```javascript
/*Action 타입 선언*/
const INCREMENT = "INCREMENT";
const DECREMENT = "DECREMENT";

/*이후 컴포넌트에서 호출해서 사용할 때, 재사용할 수 있도록 export*/
export const increment = () => {
    return {
        type: INCREMENT,  
    };
}

export const decrement = () => {
    return {
        type: DECREMENT,  
    };
}

/*Counter.js에 적용될 State 초기 설정*/
const initialState = {
    number : 0,
};

/*리듀서 설정*/
/*state는 초기 설정해놨던 state로 설정하고 action 객체를 넣어줌*/
/*switch문을 통해 action에 따라 어떻게 행동 할지 정해줌*/
export default function counter(state = initialState, action){
    switch(action.type){
        case INCREMENT:
            return {
                number: state.number + 1,
                /*기존의 state를 건드리는게 아닌 새롭게 return*/  
            };
        case DECREMENT:
            return{
                number: state.number -1,
                /*기존의 state를 건드리는게 아닌 새롭게 return*/  
            };
        default:
            return state;
    }
}
```

사용하다 보면 여러가지 redux를 하나로 합쳐야 할 때도 있을텐데 그럴 땐 combine Reducer를 사용한다.
```javascript
import { combineReducers } from "redux";
import counter from "./counter";

//import한 리듀서 이름을 그대로 사용
export default combineReducers({
  counter,
});
```

```javascript
import { combineReducers } from "redux";
import counter from "./counter";


export default combineReducers({
//import한 리듀서의 별칭을 주고 싶을 때
  counterReducer: counter,
});
```

이렇게 기본적인 리듀서를 만들었으니, 한 번 사용해보자!
number를 뿌려주고 증가, 증감하는 화면을 만들어보자
```javascript
import React from 'react'

function App(){
  return(
      <>
        <div>
          <div>number를 뿌려줄 위치</div>
          <div><button>INCREMENT</button></div>
          <div><button>DECREMENT</button></div>
        </div>
      </>
    );
}
export default App
```

![image](https://user-images.githubusercontent.com/88364980/234194052-5934961a-b94b-4f1a-932c-e659d794508d.png)
위와 같은 화면을 만들고.. 리덕스를 적용 해보나 했더니
![image](https://user-images.githubusercontent.com/88364980/234196391-20461337-89b9-4c64-ae6b-24c78a0b2bab.png)

Uncaught Error: could not find react-redux context value; please ensure the component is wrapped in a <Provider>
오류가 났다.
<Provider>로 감싸 주라는거 같은데... 문서를 찾아보니 Store를 만들고 Provider로 감싸야한다는건데
여태까지 내가 봤던 구글링 문서는 무엇이던가..? ~~아마 redux의 버전에 따른 내용 차이이려나 내 지식 오류가 아니길~~

1. 저장시킬 store를 만들어 주어야 함. (근데 1프로그램당 store는 하나밖에 없으니 주의)
2. Provider를 사용해야 함
3. 아 createStore를 하면 권장하지 않는 다는 취소선이 생기는데, legacy도 기능은 같으니 legacy 이용해서 알리아스 사용해서 깔끔하게 선언해줬음.

**main.tsx**
```javascript
import React from 'react'
import ReactDOM from 'react-dom/client'
import App from './App'
import rootReducer from './store/modules/reducers/rootReducer'
import { legacy_createStore as createStore} from "redux";
import { Provider } from "react-redux";

const mainStore = createStore(rootReducer);
ReactDOM.createRoot(document.getElementById('root')).render(
  <React.StrictMode>
    <Provider store={mainStore}>
      <App/>
    </Provider>
  </React.StrictMode>
)
```


**App.tsx**
```
import React from 'react'
import { useDispatch, useSelector } from 'react-redux';
import { increment, decrement } from './store/modules/reducers/counter';

function App(){
  const dispatch = useDispatch();
  const count = useSelector((state) => state.counter.number);
  return(
      <>
        <div>
          <div>{count}</div>
          <div><button onClick={() => dispatch(increment())}>INCREMENT</button></div>
          <div><button onClick={() => dispatch(decrement())}>DECREMENT</button></div>
        </div>
      </>
    );
}
export default App
```

**counter.js**
```javascript
/*Action 타입 선언*/
const INCREMENT = "INCREMENT";
const DECREMENT = "DECREMENT";

/*이후 컴포넌트에서 호출해서 사용할 때, 재사용할 수 있도록 export*/
export const increment = () => {
    return {
        type: INCREMENT,  
    };
}

export const decrement = () => {
    return {
        type: DECREMENT,  
    };
}

/*Counter.js에 적용될 State 초기 설정*/
const initialState = {
    number : 0,
};

/*리듀서 설정*/
/*state는 초기 설정해놨던 state로 설정하고 action 객체를 넣어줌*/
/*switch문을 통해 action에 따라 어떻게 행동 할지 정해줌*/
export default function counter(state = initialState, action){
    console.log("여기 타긴탐");
    console.log(action.type);
    switch(action.type){
        case INCREMENT:
            return {
                number: state.number + 1,
                /*기존의 state를 건드리는게 아닌 새롭게 return*/  
            };
        case DECREMENT:
            return{
                number: state.number -1,
                /*기존의 state를 건드리는게 아닌 새롭게 return*/  
            };
        default:
            return state;
    }
}
```

**rootReducer.js**
```javascript
import { combineReducers } from "redux";
import counter from "./counter";
const rootReducer = combineReducers ({
    counter
});

export default rootReducer
```

이럼 기본적인 Redux 사용 끝!
