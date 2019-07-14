---
layout: post
title: "스텍 프레임"
date: 2019-07-14 14:31:21 +0900
categories: [korean, reversing]
---

This post is a Korean translated version of [Stack Frame - Function Prologue](https://kim-yeon-gyu-exlock.github.io/reversing/2019/06/24/Reversing15.html), [Stack Frame - Function Epilogue](https://kim-yeon-gyu-exlock.github.io/reversing/2019/06/24/Reversing16.html).
ESP 레지스터는 스택의 윗부분을 가리키고, EBP는 스택의 바닥부분을 가리킨다.  
그리고 스택은 LIFO(Last in, First Out) 구조를 갖고있다.

아무튼 오늘은 메모리의 스택 영역과 관한 이야기를 해볼것이고, 좀 더 자세히 말하자면 스택 프레임에 대해 이야기를 나눌 예정이다.

# 그래서 그게 뭔데?

스택프레임은 로컬 변수, 파라미터(함수의 인자값), ESP대신 EBP를 통해 반환 주소를 저장하는 기법이다.  
그래서 이것들에는 함수 프롤로그와, 함수 에필로그라는것이 있다.

## 함수 프롤로그

함수가 호출되면, 함수 실행이 끝나고 난 뒤 스택의 위치를 어디로 돌릴지 저장해야 한다. 그래야 함수가 실행되기 전의 내용들을 제대로 접근 할 수 있을테니까.  
이것을 함수 프롤로그 라고 한다. 함수가 실행되면, 함수의 맨 위에는 다음과 같은것들이 있다.

```
push ebp
mov ebp, esp
```

이 명령어들을 이해하기 위해서는, 다른 함수를 위한 또 다른 공간을 스택위에 "쌓는다" 라고 이해하면 될것이다.  
먼저, 함수가 끝났을때 돌리기 위한 스택 바닥의 주소를 저장한다.  
그리고 두번째 명령어는 스택에서 가장 높았던 부분을 바닥으로 지정함으로써 새 공간을 쌓는 역할을 하게 만드는것이다.  
이것을 통해 함수는 지역변수를 가질 수 있게 된다.

## 함수 에필로그

그리고 함수가 끝났을때는, 전과 같이 복구되어야 한다. 이를 담당하는 코드는 다음과 같다.

```
mov esp, ebp
pop ebp
```

함수 프롤로그에서 ebp를 esp로 지정했기 때문에 그 반대로 esp에다가 그 값을 넣어주고, 스택에 진즉 쌓아둔 주소값(함수가 실행될때 들어간 ebp값)을 ebp에 넣어 줌으로써 원래의 스택 상태로 돌려놓는다.
