---
layout: post
title: "트랜지스터에서 웹 브라우저까지: 지오핫 글 번역: 2편"
date: 2019-08-30 13:20:00 +0900
categories: [translation]
---

I translated the content of [this markdown](https://github.com/geohot/fromthetransistor), if you think that there's any problem with this post, such as the licensing problems, contact me to code.yeon.gyu@gmail.com, so I can help you.

## 섹션 2: 워밍업: 하드웨어가 무슨 언어로 작성되어있나? -- 0.5 주

- LED 깜빡이기(Verilog, 10) -- 당신의 첫 프로그램입니다! 시뮬레이터가 작동하도록하는것을 배우고, 베릴로그에 대해 배웁니다.
- UART(범용 비 동기화 송수신기)만들기(Verilog, 100) -- 베릴로그의 입문 단계입니다. 진짜 UART를 복제하고, MMIO(메모리 맵 입출력)의 개념에 대해 소개합니다. 비록 시리얼 포트가 세미호스팅이긴 하지만요.(세미호스팅이란 ARM을 대상으로 한 코드가 디버거를 돌리는 호스트 컴퓨터에서 입출력장비를 사용할수 있게 해주는 메커니즘을 말합니다.) 시리얼을 테스트하는 프로그램과 led를 조절하는 프로그램을 만듭니다.

## 섹션 3: 프로세서: 그래서 프로세서가 뭔데? -- 3 주

- 어셈블러 코딩하기(Python, 500) -- 단순하고 지루한 어셈블러를 파이썬에서 작성합니다. CPU제작과 함께 병렬적으로 합니다. ARM 어셈블리를 가르쳐 줄것입니다. 처음의 결과물들은 그저 이진파일이겠지만, 당신이 링커를 작성하면 달라집니다.
- ARM7 CPU제작 (Verilog, 1500) -- 이건 하위 단계로 나누세요. 간단한 파이프라인에서 시작해서, decode, fetch, 실행까지요. 우리는 얼마나 많은 BRAM(블럭 램)을 갖고있을까요? 최소한 1MB이고, DDR로는 어려울거같고, 아마 SRAM일겁니다. 시뮬레이션 가능하고 합쳐지는게 가능하죠(synthesizable).
- 부트롬 코딩(Assembler, 40) -- 이것은 코드를 램에 시리얼 포트를 통해 다운로드 하는것을 가능하게 해주고, FPGA이미지로 구워집니다. 귀여운 테스트용 프로그램들은 여기서 작동할것이에요.
