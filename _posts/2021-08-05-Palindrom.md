---
title: [Algorithm] Palindrome(팰린드롬)
published: true
---

# [](#header-1)<알고리즘>Palindrome(팰린드롬)

Palindrome이라는 알고리즘은 숫자의 각 자릿수를 가운데 기준으로 대칭하여 서로 같은 값인지를 확인하는 알고리즘이다.<br>
처음엔 양수와 음수, 한자리인지 짝수인지 음수인지에 대해 기준을 나눴었다.

![팰린드롬](https://user-images.githubusercontent.com/54430432/128285238-646de14d-7fba-45f9-a1f9-c161e220a94f.PNG)

↑ 직접 코딩했던 부분

![팰린드롬 해답](https://user-images.githubusercontent.com/54430432/128285276-fbe13e69-183e-4709-bfa7-12f4dd5c11d0.PNG)

↑ 부장님께서 보여주신 해답

굳이 배열을 쓰지 않고서 변수에 할당해서 바로바로 사용하면 되는데 왜 메모리를 낭비해서 만들었던건지 효율성이 떨어지게 <br>
(물론 안되는건 아니다.) <br>
좀 더 간단하고 효율적으로 쓸 수 있도록 노력해보자 <br>