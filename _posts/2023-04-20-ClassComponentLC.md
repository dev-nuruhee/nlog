---
title: React - Rendering part1 클래스 컴포넌트의 생명주기 (Class Component Life Cycle)
published: true
---
### 1. Class Component Life Cycle ###

우리는 지난 포스팅에서 Component의 종류가 두가지가 있다는 것을 배웠다.
Class Component와 Functional Component
주로 Functional Component를 사용하겠지만, Class Component를 언제 만날지 모르니 둘 다 학습을 해야하겠지?

이번 포스팅에서는 Class Cmponent Life Cycle에 대해서 서술해보고자 한다.

Life Cycle은 라이프사이클 즉 생명주기라고도 하는데 개발을 좀 해본 개발자들이라면 필요성에 대해 알 것이다.
어떠한 변수들이 언제 생성되고 언제 사라지고에 따라 코딩하는 방향성이 많이 달라질 것이니 충분한 이해가 필요하다.
~~(나는 이 부분이 제일 중요하다고 생각하기도 하는데..)~~

무튼 알다시피 리액트 Class Component를 사용하기 위해선 Component를 Extend 받아야한다.
모르시는 분들은 https://dev-nuruhee.github.io/nlog/ClassVSFunctionalComponent 참조

``` javascript
class Welcome extends Component {
  render() {
    return <h1>Hello, World ! </h1>;
  }
}
```

Class Component의 생명주기는 크게 3부분으로 나뉜다.
Mounting -> Updating -> Unmounting

Mount에선 무얼하고 Update에선 무얼하고 Unmount에선 무얼 하는지 알아보자!

![Image](https://user-images.githubusercontent.com/88364980/233240350-74d23bdf-a0e3-43da-9932-10471731a70e.png)

위와 같은 용도로 Mount에선 진행되는데 그림만 보고선 뭔소린지 모르니까 실제 코드로 살펴봐야지?

```
/*Contructor*/
class Welcome extends Component{
  constructor(props){
    super(props); /*this.props를 사용하지 말고 super(props)를 권고*/
    this.state = {counter: 0} /*contructor에서만 state는 변경 가능 다른 부분에선 setState() 함수로 변환한다!*/
  }
  
  render(){
     return <h1>Hello, World ! </h1>;
  }
}
```
위의 그림에서는 this.props를 사용한다고 하긴 했는데 찾아보니 버그 발생 위험이 있어서 (생성자 내에서 정의 되지 않아서)
super(props)를 권고한다고 한다.

부모클래스의 생성자를 호출해서 내부의 state를 초기화 하는 용도로 사용하는 것이다.
그럼 다음 단계인 getDeriverdStateFromProps 함수를 살펴보자.
getDeriverdStateFromProps 함수는 static과 함께 사용되며 말 그대로 props에서 state를 받아오는 것이다.
아래 추가된 코드를 보자.

```
class Welcome extends Component{
  constructor(props){
    super(props);
    this.state = {counter: 0} 
  }
  /*getDeriverdStateFromProps()*/
  static getDerivedStateFromProps(nextProps, prevState) {
  if (nextProps.value !== prevState.value) { /*State를 직접 설정하는 것이 아닌 특정 props가 설정될 때 state를 리턴하는 형태로*/
    return { value: nextProps.value };
  }
  return null;
  }
  render(){
     return <h1>Hello, World ! </h1>;
  }
}
```
render의 설명은 별다를게 없을것 같고 render가 돌아가는 원리를 알고 싶다면 아래 문서를 확인하시라..
https://ko.reactjs.org/docs/rendering-elements.html

그럼 Mount의 마지막 단계인 ComponentDidMount를 보자.
화면을 다 그리고 나면 해줘야 할 내부 기능들이 있을수도 있다.
그땐 ComponentDidMount를 사용하면 된다.
~~아마 functional Component에서는 Hook을 이용해 useEffect 쓰겠지?~~

```
class Welcome extends Component{
  constructor(props){
    super(props);
    this.state = {counter: 0}
  }
  static getDerivedStateFromProps(nextProps, prevState) {
  if (nextProps.value !== prevState.value) { 
    return { value: nextProps.value };
  }
  return null;
  }
  componentDidMount(){
        console.log("랜더링이 끝나면 호출됩니다.");
  }
  render(){
     return <h1>Hello, World ! </h1>;
  }
}
```

자 이렇게 하면 ClassComponent의 Mounting에 대한 이해는 끝났다.
Functional Component의 LifeCycle도 이해해야 하고 Updating, UnMounting의 대한 부분도 해야한다.
그래도 좀 더 해보자 ~~네가 선택한 개발 악으로 깡으로 버텨라~~

첫 화면을 랜더링하고 나서 state나 props가 변경될 수가 있다.
그렇다면 새로운 랜더링이 필요할 것이 아닌가?
더군다나 상위 Component가 바뀌면 하위 Component들도 새로 마운트가 되어야하니까 말이다.
이 때 사용되는 것이 바로 Updating이다.

![Image](https://user-images.githubusercontent.com/88364980/233251171-89b8b264-3b60-457d-80f3-d24e6fc8a9b1.png)


getDerivedStateFromProps() 함수와 render() 함수는 위에서 설명했으니 생략.

```
/*shouldComponentUpdate*/
shouldComponentUpdate(prevProps, prevState) {
    return this.props.data !== prevProps.data;
  }
```
이전의 props와 다를 경우에만 랜더링 될 수 있도록 설정하면 최적화가 이루어짐.
~~물론 항상쓰면 좋겠지만 이전과 다르지 않아도 랜더링이 필요한 경우가 있을수 있으니 내장되어 항상 실행되지 않겠지?~~

다음으로는 getSnapshotBeforeUpdate와 componentDidUpdate를 살펴보자
마지막으로 랜더링 된 결과가 반영되기 전에 호출하고 반환값을 인자로 받은 후에 재랜더링이 이루어질 시 해야할 동작들을 기술하는 부분이다.
잘 쓸일이 없을거 같긴한데 늘 언젠가 한 번은 쓰게 되니 간단하게 함수 어떻게 사용하는지만 보고 넘어가자.
```

getSnapshotBeforeUpdate(prevProps, prevState) {
    /*이전 props의 값과 props의 값이 다르다면 value return/*
    if (prevProps.value !== this.props.value) {
        return prevProps.value;
    }
    return null;
}

componentDidUpdate(prevProps, prevState, snapshot) {
    if (snapshot == prevProps.value) {
      console.log("업데이트 되기 직전의 값: ", prevProps.value);
    }
  }
```

마지막으로 Unmounting 부분이있다.
더는 컴포넌트를 사용하지 않을 때(DOM상에서 제거 될 때)발생하는 이벤트가 있고 그 이벤트를 발생시키는 함수는 바로 componentWillUnmount이다.

```
componentWillUnmount(){ /*컴포넌트를 제거하는 과정이기에 setState()를 사용해서는 안됨*/
    console.log("해당 컴포넌트는 제거됩니다..");
}
```

그 외 오류를 처리하는 방법들
```
  static getDerivedStateFromError(error) {
    // state를 갱신하여 다음 렌더링에서 대체 UI를 표시합니다.
    return { hasError: true };
  }
```

```
  componentDidCatch(error, info) {
    // Example "componentStack":
    //   in ComponentThatThrows (created by App)
    //   in ErrorBoundary (created by App)
    //   in div (created by App)
    //   in App
    logComponentStackToMyService(info.componentStack);
  }
```
