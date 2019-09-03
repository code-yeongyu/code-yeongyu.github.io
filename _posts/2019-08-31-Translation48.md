---
layout: post
title: "트랜지스터에서 웹 브라우저까지: 지오핫 글 번역: 3편"
date: 2019-08-31 11:03:00 +0900
categories: [translation]
---

I translated the content of [this markdown](https://github.com/geohot/fromthetransistor), if you think that there's any problem with this post, such as the licensing problems, contact me to code.yeon.gyu@gmail.com, so I can help you.

#### 섹션 4: 컴파일러: 고수준 프로그래밍 언어 -- 3 주

- C언어 컴파일러 만들기(Haskell, 2000) -- 조금 더 재밌는 과정입니다. 이 과정을 통해 컴파일러의 기초적인 설계에 대해 공부 할 수 있게 됩니다. 하스켈로 작성하도록 합니다. 파서를 작성하도록 합니다. 이것을 서브챕터로 나누세요. 결과물이 ARM 어셈블리로 나옵니다.
- 링커 만들기(Python, 300) -- 당신이 똑똑하다면, 하루정도 걸릴겁니다. ELF파일이 출력값으로 나옵니다. QEMU와 테스트 하는데 사용해요, 세미호스팅으로요.
- libc + malloc(C, 500) -- 복잡한 프로그램을 위한 관문입니다. 여기서 Libc는 절반만 구현합니다. memcpy나 memset, printf같은걸요. 그치만 시스템콜 wrapper는 만들지 않습니다.
- 이더넷 컨트롤러 제작(Verilog, 200) -- 진짜 PHY(이더넷 물리 계층)에 접근합니다, MMIO 설게를 매우 조심스럽게 고려하면서요.
- 부트로더 작성(C, 300) -- UDP를 통한 통신을 하는 이더넷 프로그램을 부트로더에 작성합니다. C로 짜여질것입니다. Maybe don’t redownload over serial each time and embed in FPGA image. (해석 실패...)
