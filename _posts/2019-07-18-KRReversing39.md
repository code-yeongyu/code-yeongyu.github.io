---
layout: post
title: "Reversing.kr Easy Crack 라이트업"
date: 2019-07-18 9:21:00 +0900
categories: [reversing, korean]
---

This post is a Korean translated version of [Reversing.kr Easy Crack writeup](https://kim-yeon-gyu-exlock.github.io/reversing/2019/07/17/Reversing38.html).

# Reversing.kr ?

Reversing.kr 은 한국인 리버서들에게 유명한 사이트이다.
윈도우, 리눅스, 심지어는 macOS를 위한 리버싱 문제들도 준비되어있는 그런 사이트이다.

어쨌든, 오늘 풀어보는것은 Reversing.kr에서의 첫 문제다.  
일단 실행파일을 다운로드 받자.  
[이곳](http://reversing.kr/)에서 모든 문제들을 구할수 있다!

그래서 이번 문제는 내가 적은 string과 정답을 비교하는 간단한 프로그램이다.
![easycrack_1](https://raw.githubusercontent.com/kim-yeon-gyu-exlock/kim-yeon-gyu-exlock.github.io/master/assets/pictures/easycrack_1.png)  
![easycrack_2](https://raw.githubusercontent.com/kim-yeon-gyu-exlock/kim-yeon-gyu-exlock.github.io/master/assets/pictures/easycrack_2.png)

올릳디버거로 열어봤더니, 다음과 같았다.  
![easycrack](https://raw.githubusercontent.com/kim-yeon-gyu-exlock/kim-yeon-gyu-exlock.github.io/master/assets/pictures/easycrack.png)  
처음봤을땐 VB코드인가? 싶었는데 지금 보니까 또 STUB코드가 더럽지 않은 모습을 봐서는 C/C++ 코드인것 같기도하고.. 잘 모르겠다.

어쨌든 올리디버거의 기능인 바이너리 내의 string을 찾아주는 기능으로 좀 봤더니 다음과 같았다.
![easycrack_strings](https://raw.githubusercontent.com/kim-yeon-gyu-exlock/kim-yeon-gyu-exlock.github.io/master/assets/pictures/easycrack_strings.png)  
그림에서 보는것처럼, 내가 입력한 문자열이 맞는지 틀린지 결정하는 부분의 코드가 좀 있는것같았다.  
그리고 이게 검사하는 부분이다.  
![easycrack_firsttotwo](https://raw.githubusercontent.com/kim-yeon-gyu-exlock/kim-yeon-gyu-exlock.github.io/master/assets/pictures/easycrack_firsttotwo.png)

난 이미 풀었기 때문에 주석이 있고, 원래는 없다는 점을 참고하자.  
첫번째 CMP부분은 그냥 감으로 풀었다.  
16진수 61이 해커스쿨을 풀다보니 너무 나에게 친숙해서, 그냥 입력필드에 "aaaaa"를 입력했더니 첫번째 검사 부분에서 통과했다.  
"1234a" 부터 "1a345"까지 시도한 끝에, 그것이 [argument+1] 이 'a'인지 아닌지 검사하는 부분이라는것을 알았다.

그리고 이제 두번째 부분.  
![easycrack_two](https://raw.githubusercontent.com/kim-yeon-gyu-exlock/kim-yeon-gyu-exlock.github.io/master/assets/pictures/easycrack_two.png)  
주석에 오류가 있는데, argument+3가 아니라 argument+2이다.

레지스터 패널에서 "345"를 출력하고 있길래 대충 c에서 이런 코드겠거니 했다.

```c
strncmp([argument+2], "5y", 2);
```

그리고 맞았다. "1a5y56789"를 입력함으로써 통과했다.  
다음 부분을 보자.  
![easycrack_three](https://raw.githubusercontent.com/kim-yeon-gyu-exlock/kim-yeon-gyu-exlock.github.io/master/assets/pictures/easycrack_three.png)  
바로 직전의 확인 부분과 굉장히 비슷해보이는 코드가 있다.  
아까 그랬던것처럼, 레지스터 패널에서 "56789"를 보아서, 대충 이런 코드인가 싶었다.

```c
strncmp([argument+3], "R3versing", 9);
```

그래서 "1a5yR3versing"을 입력했을때 이번 검사를 통과 할 수 있었다.  
이제 마지막 부분이다!  
![easycrack_four](https://raw.githubusercontent.com/kim-yeon-gyu-exlock/kim-yeon-gyu-exlock.github.io/master/assets/pictures/easycrack_four.png)  
esp+4와 16진수 45, 그러니까 아스키로 'E'를 비교하고있다.  
스택 영역에서 볼 수 있듯, esp+4 는 내가 입력한 문자열이 있는곳이다. 그러니 페이로드는 다음과 같다.

```
Ea5yR3versing
```
