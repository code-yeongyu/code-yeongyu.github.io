---
layout: post
title: "트랜지스터에서 웹 브라우저까지: 지오핫 글 번역: 6편"
date: 2019-09-03 20:56:00 +0900
categories: [Plans]
---

I translated the content of [this markdown](https://github.com/geohot/fromthetransistor), if you think that there's any problem with this post, such as the licensing problems, contact me to code.yeon.gyu@gmail.com, so I can help you.

#### 섹션 7: 물리적으로: 직접 하드웨어에서 돌려봅시다 -- 1 주

- FPGA 다루기(C, 200) -- JATG(디지털 회로에서 특정 노드의 디지털 입출력을 위해 직렬 통신 방식으로 출력 데이터를 전송하거나 입력데이터를 수신하는 방식)으로 비트뱅잉을 하기 위한 적은 양의 코드를 작성합니다.
- FPGA보드 제작 -- 보드 설계, FPGA BGA reflow, FPGA flash, 50mhz 클럭과, JTAG USB포트, 그리고 flasher(특별한 하드웨어가 아닙니다, JTAG를 하기 위한그저 작은 사이프러스 사의 USB요), 적은수의 led, 리셋버튼, USB를 통해 전원이 공급되는 시리얼포트(USB-FTDI), SD카드, 확장 커넥터(ide cable?), 그리고 이더넷 포트요. 옵션이긴한데, 확장보드, 호스트 USB포트, NTSC TV 출력, ISA port, 그리고 당신을 조롱하기위한 PS/2포트도 있습니다. 우리는 reflow를 하기 위한 토스터기와 멀티미터 온도계를 제공합니다.
- Bringup -- 컴파일 후 보드에 다운로드 합니다.

5일에 걸쳐 짬짬히 지오핫의 글을 번역하였습니다. 제 영어실력이 부족한 관계로 매끄러운 번역이 어려웠네요. 사실은 아직까지도 제대로 이해하지 못한 부분이 꽤 있습니다.  
그러나 이 글을 번역하면서 약간 전자공학? 적인 부분에 대해서 전혀 몰랐던 용어들, 예를들면 JTAG, FPGA, Verilog와 같은것들에 대해서 알 수 있게 된게 큰 성과가 아닌가 싶습니다.  
만약 제가 대학교를 진학하지 않겠다라는 생각이 확고해지면, 지오핫이 말한 그러한 내용들을 공부해야겠지요.  
그렇게 된다면 제가 공부한 자료들도 이 블로그에 올리겠습니다. 지오핫이 올린글에서는 단순히 '뭘 어떻게 공부해라' 만 제시할뿐, '어디에서 무엇을 보고 공부하라'는 제시하지 않거든요.  
시간이 날때, 이 글들의 용어들을 다시한번 정리하고 각주를 좀 더 많이 달아서 읽기 편하실 수 있도록 하겠습니다.
