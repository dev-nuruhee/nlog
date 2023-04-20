---
title: React - Rendering part2 함수형 컴포넌트의 생명주기 (Functional Component Life Cycle)
published: true
---
### 2. Functional Component Life Cycle ###

지난 포스팅에서 Class Component의 Life Cycle을 알아봤다.
하지만 Functional Component에선 Hook을 사용하게 되면서 차이가 생기게 되었다.
Hook은 Class Component의 모든 것을 호환하는가? 호환하지 않는 부분은 어떻게 해야하는가?가 이번 포스팅의 중점이다.
Hook의 상세한 사용 방법은 따로 포스팅 하겠다!

Mount에서의 차이
![image](https://user-images.githubusercontent.com/54430432/233275954-2330f312-321b-4d85-8504-197ac11607f4.png)

getDerivedStateFromProps는 Prop에서 state를 return하여 받는 부분인데 이 부분은 Hook에서 지원하지 않는다.
그래서 이 부분은 직접 구현해야 하는데, 공식 문서에서 제공한 것 처럼 아래 코드를 확인해보자
```
function ScrollView({row}) {
  const [isScrollingDown, setIsScrollingDown] = useState(false);
  const [prevRow, setPrevRow] = useState(null);

  if (row !== prevRow) {
    // 마지막 렌더링 이후 행이 변경되었습니다. isScrollingDown을 업데이트합니다.
    setIsScrollingDown(prevRow !== null && row > prevRow);
    setPrevRow(row);
  }

  return `Scrolling down: ${isScrollingDown}`;
}
```

Update에서의 차이
![image](https://user-images.githubusercontent.com/54430432/233280910-94a5adaf-98d3-4c29-8449-5b7afd513ff1.png)

미지원되는 것들이 많은데 왜 Class Component에서 Functional Component로 바꿔서 Hook에다가 직접 코드를 짜야하는 수고를 덜어가며 방향성을 바꾼다고 말하면.. 나는 이렇게 말할 수 있다.

~~Hook에서 지원하는 기능들이 훨씬 많고 전체적인 일의 능률이 올라가! 코드의 질이나 간편성이 늘어나지!~~
라고 말하겠지만.. 늘 새로운 기술에 적응해야한다는 건 참 쉽지 않은 일이다 'ㅠ'

Hook은 차후에 다시 이야기 하고 그럼 미지원되는 부분들은 어떻게 처리할 것인가를 보자!

getDerivedStateFromProps는 위에서 코드를 직접보여줬고, shouldComponentUpdate는 최적화를 위해서 사용한다고 했었다.
아래와 같이 React.memo를 통해 가볍게 만들 수 있다고 한다.
```
const Button = React.memo((props) => {
});
````

getSnapshotBeforeUpdate 같은 경우는 구글링 해봤는데 마땅히 없고 직접 구현을 해야할 것으로 보인다.

마지막 단계인 unmount같은 경우는 useEffect로 대체 가능하다.

그렇다면 이제 우리는 차이를 알아봤으니 실질적으로 사용하기 위해서 Hook에 대해서 알아보자!



