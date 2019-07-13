---
layout: post
title: "바이트 순서, 레지스터"
date: 2019-07-13 12:23:45 +0900
categories: [korean, reversing]
---

- This post is a Korean translated version of [Byte Ordering, Registers](https://kim-yeon-gyu-exlock.github.io/reversing/2019/06/17/Reversing8.html), [Other Registers](https://kim-yeon-gyu-exlock.github.io/reversing/2019/06/18/Reversing9.html), [Miscellaneous tips I've learned today](https://kim-yeon-gyu-exlock.github.io/reversing/2019/06/26/Reversing17.html).

# 바이트 순서 - 리틀 엔디안, 빅 엔디안

변수를 만들고 그 곳에 0x123456 이라는 값을 넣었다고 치자.

## 빅 엔디안

빅 엔디안에서는, 우리가 보는 방식 그대로 데이터가 보일것이다.  
그래서, 빅 엔디안은 우리가 정보를 저장하는 방식이라고 할 수 있다.  
즉,

```
0x123456
```

그대로 들어갈것이고 그대로 볼 수 있을것이다.

## 리틀 엔디안

리틀 엔디안에서는 데이터의 순서가 바뀐다. 그래서, 0x123456은 보통 이런식으로 표기하곤한다.

```
\x56\x34\x12
```

이런식으로 말이다.

# 레지스터

‘Basic Program Execution Register’, 라고 불리는 레지스터들은 총 네개가 있는데, 이들은 다음과 같다.

- General Purpose Registers, 범용 목적 레지스터 (8개의 32비트 레지스터로 구성됨)
- Segment Registers, 세그먼트 레지스터 (6개의 16비트 레지스터로 구성됨)
- Program Status and Control Register, 프로그램의 상태와 조절 레지스터 (32비트 레지스터 하나)
- Instruction Pointer, 명령 레지스터 (32비트 레지스터 하나)

## 범용 목적 레지스터

- EAX: 명령에서 누산기(계산 결과를 저장하는 곳) 역할과 결과값을 저장하는 레지스터
  - 함수를 실행 한 뒤 종료할 때 반환값을 저장하는 용도로도 쓰이고, [Miscellaneous tips I've learned today](https://kim-yeon-gyu-exlock.github.io/reversing/2019/06/26/Reversing17.html)이곳에서 내가 감탄했던 바와 같이 값을 더하거나 빼는 연산을 하고 그 값을 반환하는 코드의 경우에는 그냥 값을 더한뒤 바로 함수를 종료한다. (이미 더한 값이 EAX에 있으니까 그냥 종료해도 반환 값이 반환된다.)
- EBX: 데이터 세그먼트(메모리의 데이터 영역)에 있는 데이터를 가리키는 레지스터
  - ESI와 EDI 레지스터와 함께 인덱스에 접근할 때 쓰인다.
- ECX: String과 반복 작업을 실행할 때 (반복문) 카운터로 사용된다.
  - ‘for(int i = 0;i<3;i++);’와 같은 코드에서 사용된다고 이해하면 되겠다.
- EDX: 입출력 포인터
  - 입출력포인터의 값을 저장하는데 쓰인다고 한다.

## 세그먼트 레지스터

세그먼트는 메모리의 부분들을 나눠 시작주소를 매기고, 권한등을 주는 방식으로 메모리를 보호하는 방법이다.
또한, 페이징 방법이라는것을 사용해 물리적인 메모리 안에 가상 메모리라는것과 함께 사용되곤한다.
세그먼트 메모리의 주소들은 Segment Decriptor Table에 있고, 세그먼트 레지스터는 이러한 SDT의 인덱스를 가리킨다.

세그먼트 레지스터는 총 6개의 16비트로 구성되어있다.

- CS, Code Segment
- SS, Stack Segment
- DS, Data Segment
- ES, Extra Segment
- FS, Data segment
- GS, Data segment

## 프로그램 상태와 조절 레지스터

EFLAGS 레지스터라고도 불리며, 32비트 레지스터이다.  
이름처럼 0은 꺼짐을, 1은 켜짐을 의미하며 각각의 비트는 각각 다른것의 플래그역할을 한다.  
내가 읽는 책인 리버싱 핵심원리에서는 초심자 단계에서 32비트의 플래그 전부를 공부하는것은 어렵다고 하고, ZF, OF, CF 같은 응용 프로그램 리버스 엔지니어링의 필수적인것들만 공부하라고 하더라.

- ZF, Zero Flag
  - 계산 명령의 결과값이 0일때 1로 바뀐다.
- OF, Overflow Flag
  - 부호가 있는 정수형에서 오버플로우가 날때 1로 변한다. MSB(Most Significant Bit)라는게 바뀔때도 값이 바뀐다고 하더라.
- CF, Carry Flag
  - OF랑 같으나 부호가 없는 정수형용이다.

## 명령어 레지스터

EIP라고 불리며, 32비트 레지스터이다.  
현재 실행중인 명령의 주소를 가리킨다.  
다른 범용 레지스터들과 달리, 수정이 불가능하다.  
유일하게 내가 원하는 값으로 바꾸는 방법은 분기문(jmp, ret 등)을 사용하는것 뿐이다.
