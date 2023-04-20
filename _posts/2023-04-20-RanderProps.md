---
title: React - Rendering part3 리스트와 키
published: true
---

배열을 구성하는 방법은 일반적으로 같은데 보통 예제가 화살표 함수로 쓰는 것 밖에 없더라.. 

~~나는 for문을 주로 쓰는 5년차 개발자인데..~~ 

리스트를 구성할 때 키를 주입하고 화면에 뿌리는 예제를 구현해봤다.

```
function App() {
  const numbers = [1, 2, 3, 4, 5]; /*배열을 만들고*/
  let doubled = []; /*빈 배열을 선언해주고*/
  for(let i=0; i<numbers.length; i++){
    doubled[i] = <li key={numbers[i].toString()+"입니다"}>{numbers[i]*2}</li>; 
    /*배열에 html과 같이 삽입해준다 실제값은 {}를 함께 쓰면 된다./*
  }
  
  return (
    <>
        <ul>
          {doubled}
        </ul>
    </>
  )
}

export default App
```

뭐 이런 형식인데 공식 문서보니까 요소 하나에 key를 무조건 삽입을 해줘야 하는듯? 안해도 랜더링은 되는데 콘솔에 오류남!
