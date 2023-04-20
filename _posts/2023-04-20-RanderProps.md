---
title: React - Rendering part4 Rander Props
published: true
---

나는 기존에 Vue를 사용했기에 Props라는 개념을 알고 있다.  

일단 React에서 처음 이 개념을 보는 사람들을 위해 간단하게 설명해보자면..  

일반적으로 부모컴포넌트 아래에 여러개의 자식 컴포넌트를 가지고 있다. 

부모컴포넌트에서 자식 컴포넌트로 값을 넘겨야 하는 상황이 있는데 값을 넘기기 위해 사용하는 기능이 props이다. 

토이프로젝트에서 만든 props의 사용예를 보면

```
import React from 'react'
import TopTitle from '../components/TopTitle'
import OnedepthImg from '../components/OnedepthImg';

function FirstDepth(){ /*부모 컴포넌트*/
  return(
    <>
      <TopTitle titleValue="성별을 골라주세요."></TopTitle> /*자식 컴포넌트/*
      <OnedepthImg/>
      
    </>
  )
 }

 export default FirstDepth;

 ```

 위와 같은 코드가 있다.
 자식 컴포넌트에 "성별을 골라주세요" 라는 텍스트를 넘기려면

 ```
function TopTitle({ titleValue }) {
  return <StyledContainer><StyledDiv>{titleValue}</StyledDiv></StyledContainer>;
}
```

TopTitle이라는 컴포넌트에서도 넘기는 값을 받는다. 그리하여 자식 컴포넌트에서 사용할 수 있는데 이 개념이 바로 props이다.
