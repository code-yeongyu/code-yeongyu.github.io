---
layout: post
title: "트랜지스터에서 웹 브라우저까지: 지오핫 글 번역: 1편"
date: 2019-08-29 11:40:00 +0900
categories: [translation]
---

I translated the content of [this markdown](https://github.com/geohot/fromthetransistor), if you think that there's any problem with this post, such as the licensing problems, contact me to code.yeon.gyu@gmail.com, so I can help you.

# 트랜지스터에서 웹 브라우저까지

### 12주간의 빡센 코스

인력을 고용하는것은 어렵고, 현대의 많은 컴퓨터공학 수업은 매우 나쁘죠. 그리고 현대의 컴퓨터에 관한 내용들을 아주 기초적인 내용부터 이해하고 있는 사람들을 찾기가 어렵습니다.

이제 그것들을 다 씻어내고, 소프트웨어 중점으로 갑시다. 현실에 더 가깝게요.

## 섹션 1: 도입부: Cheating our way past the transistor -- 0.5주

- 트랜지스터에 관해서: FPGA(field programmable gate array)가 어떻게 트랜지스터를 만드는데 사용될 수 있는지, 그리고 IC(집적 회로) 들은 그저 믿을만한 패키지 안에있는 트랜지스터들이라는 것에 대해서 묘사합니다. (Look Up Table, 순람표)와 같은 내용을 이해합니다. 트랜지스터 이론에 대해 간단히 이야기 합니다만, 그러나 모든 프로젝트들은 서로가 있어야 하기때문에 뭔가를 만들 수는 없습니다.

* Emulation -- 진짜 하드웨어의 한계에 다다르는것을 만드는게 이 코스의 목표입니다. Verilator(베릴로그 시뮬레이터)와 같은것들 사용하는것은 누구든 컴퓨터와 ㄴ로 수 있도록 해줄 것 입니다.
