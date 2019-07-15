---
layout: post
title: "선린톤 준비과정"
date: 2019-07-18 03:26:18 +0900
categories:
  [
    django,
    postgresql,
    gcloud,
    development,
    programming,
    python,
    hackathon,
    korean,
  ]
---

This post is a Original Korean Post.

# 선린톤?

선린톤은 선린인터넷고등학교 해커톤의 이름으로서, 여느 해커톤 대회처럼 당일 발표되는 주제에 맞춰 개발을 하는 대회이다.  
나는 백엔드 api개발자로서 본 대회에 참여하게 되었으며, 총 12팀이 본선에 올라갔다.  
그 중 6팀이 수상을 하게되고(금1, 은2, 동3), 각 팀은 4명씩 구성이 되어있다.

# 그래서 뭘 준비하는데?

나는 장고를 사용한 개발을 하는 만큼 서버로 사용될 컴퓨터에 실행을 위한 환경을 만들어 두어야한다.  
구글 클라우드의 서버 위에다가 올려서 실시간으로 테스트를 할 예정이라, gcloud 내의 작업환경 정도를 설정해두어야 한다.

# Let's get ready!

리눅스를 사용하던 시절 미리 만들어놓은 구글 클라우드 서버가 있어서, 나는 연결만 하면 됬다.  
일단 [강좌 하나](https://jungwoon.github.io/google%20cloud/2017/10/26/install-gcloud/)를 참고하여, 내 맥에 구글 클라우드 SDK를 설정하였다.

나는 주로 postgresql을 db로서 사용하기 때문에, [이 글](https://blog.leop0ld.org/posts/python-django-use-postgresql/)을 보고 설치를 해주었고, 프로덕션 레벨의 배포를 위해 [gunicorn을 설치](https://cjh5414.github.io/nginx/)를 했다.

# 잘 하고 오겠습니다!

12팀중 6팀을 수상하기 때문에, 첫 컴퓨터 대회에서의 상을 기대해 볼 수 있을것같다!
열심히 개발하고, 즐겁게 놀다가 와야겠다.

I'm sorry that today's post is not about hacking!
