---
layout: post
title: "함수 호출 규약"
date: 2019-07-15 11:00:21 +0900
categories: [korean, reversing]
---

This post is a Korean translated version of [Calling convention](https://kim-yeon-gyu-exlock.github.io/reversing/2019/06/27/Reversing18.html).

# cdecl

cdecl 함수 호출 규약은 가변인자를 다루기에 굉장히 유용한데, 이는 다른 함수 호츌 규약에서는 구현하기 어렵기 때문이다.  
cdecl 은 함수가 끝나고 반환될때 함수의 호출자가 스택을 비우는 함수 호출 규약이다.  
![cdecl](https://raw.githubusercontent.com/kim-yeon-gyu-exlock/kim-yeon-gyu-exlock.github.io/master/assets/pictures/cdecl.png)  
보다시피, add esp, 8인것을 볼 수 있다. 함수가 호출되기전에 인자값으로 8바이트를 넘겼음을 의미한다.

![cdecl_retn](https://raw.githubusercontent.com/kim-yeon-gyu-exlock/kim-yeon-gyu-exlock.github.io/master/assets/pictures/cdecl_inside_func.png)  
그리고 RETN 명령어쪽을 보면 알겠지만, stdcall 방식이 인자값을 갖고있는데에 반해 여기서는 아무런 인자값도 RETN과 함께 있지 않다.  
C언어는 이 함수호출규약을 기본적으로 사용하지만, 함수 이름 앞에 \_\_stdcall 키워드를 넣는 방식으로 cdecl을 사용하지 않을 수 도 있다.

# stdcall

stdcall은 호출받은 함수가 retn 명령어를 실행할 때에 스택을 정리하는 방식이다.  
그래서, 위에서 보았던 ADD ESP, XXX 와 같은 명령어가 함수 실행 뒤에 실행 될 필요가 없다.  
![stdcall](https://raw.githubusercontent.com/kim-yeon-gyu-exlock/kim-yeon-gyu-exlock.github.io/master/assets/pictures/stdcall.png)  
함수가 끝날때 마다 add 명령어를 실행하지 않아도 되는 점에서 cdecl보다 이점을 갖고 있다.  
그래서 코드의 사이즈를 줄일 수 있다.
재밌는 점은, Win32API는 이 stdcall을 사용한다. c언어는 cdecl을 기본적으로 사용하는데 말이다.  
그 이유는 win32api를 델파이나 비주얼 베이직과 같은 다른 언어와 함께 사용 할 때에 호환성을 높이기 위해서 라고 한다.

# fastcall

stdcall 기반의 함수 호출 규약이다. 인자값을 넘길때 스택을 사용하는 것이 아닌(push 명령어를 통한..) ECX와 EDX를 사용하여 넘기는 방식이다.  
그래서 인자값이 두개일 경우에만 사용 가능하다.  
이름처럼, 레지스터의 속도가 메모리에 접근하는것 보다 빠르기 때문에 속도면에서 stdcall보다 유리하다.  
그렇지만 ecx와 edx를 사용하기 위해 가끔 오버헤드(추가작업)가 필요하다. 가령 ecx와 edx에 중요한 데이터를 갖고있다면 스택과 같은곳에 백업하는 작업이 필요하다.  
또한 함수 안에서 ecx와 edx가 사용될 필요가 있을 경우에도 오버헤드가 필요하다.
