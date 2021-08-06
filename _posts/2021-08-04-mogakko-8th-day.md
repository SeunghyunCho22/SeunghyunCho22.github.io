---
layout: post
title: "[모각코]8th-day"
---

8월 4일 회차에서는 오픈월드 서바이벌 게임의 유닛들 중 잡식동물을 제작해보는 시간을 가졌다.
게임 컨셉상 동물은 크게 3가지 부류로 나눌 수 있다.

1) 육식동물 - animator(idle, drink, eat(예)풀뜯기..등등)이 작동하다가 player가 View Angle(시야 각)내부에 있으면서 View Distance(시야 거리) 안에 들어오면, player에게 접근하여 공격시도를 한다.   
2) 초식동물 - animator이 작동하다가 player가 View Angle내부에 있으면서 View Distance 안에 들어오면, player을 피해 멀리 도망간다.   
3) 잡식동물 - 평상시에는 사거리와 상관없이 설정한 animator들이 작동하고 있지만, player에게 공격을 받을 시 player를 쫓아오며, 공격시도를 한다.

이를 해결하기 위해 기존에 작성했던 StrongAnimal 스크립트를 상속받는, 새로운 MAnimal 스크립트를 작성했다.

<script src="https://gist.github.com/SeunghyunCho22/14b13855ef7942bf11755e9dc8f2f001.js"></script>

스크립트를 보면, Damage를 입었을 경우(player에게 공격을 받은 경우가 해당함), 조건문으로 죽지 않았을 경우에 한하여 다른 코루틴을 stop하고
player을 쫓는 코루틴을 실행시킴을 알 수 있다.

![image](https://user-images.githubusercontent.com/78609676/128493036-f6955619-77a2-4282-9908-e299437b5be0.png)

이런식으로 각 동물에 해당하는 Animator들과 스크립트를 알맞게 설정해주면(빨간색으로 하이라이트한 부분-제작한 잡식동물들, 파란색으로 하이라이트한 부분-설정해 둔 View Angle과 View Distance),
잡식동물이 구현됨을 알 수 있다.

![image](https://user-images.githubusercontent.com/78609676/128493322-5143ca47-d64a-45b2-a53f-95a98bbc72bd.png)

   
현재 구현 완료한 잡식동물은 두마리로, 추후에 더 제작을 할 예정이고 전체적으로 animator을 자연스럽게 하기 위해 수정을 진행할 예정이다.

