---
layout: post
title: "[모각코]3rd-day"
---

3rd Mogakko.

Mission : 
1. 모바일 게임의 광고보기 버튼 만들기
  (Make an Ad View Button for Mobile Games)
2. 함정을 만들고 함정에 빠졌을때 Lose Panel, 목표 지점에 도달했을 때 Win Panel 띄우기
  (Create a trap, if fall into a trap, display "LOSE" panel on the screen. if reach the target point, display "WIN" panel on the screen.)
3. GameManager를 만들어서 winPanel과 losePanel이 true가 될때, 콘솔 창에 각각 "Win!"과 "Lose"를 출력하게 만들기.

이전 시간에 해결하지 못했던 더블점프 문제를 여전히 해결하지 못했다. PlayerMove C# Script에서 잘못된 부분을 찾아서 수정을 해야 한다.
앞서 언급한 문제로 인해, 함정을 점프하여 목표지점까지 도달하여야 확인할 수 있는 WiN panel은 확인하지 못했다. 그러나 함정에 빠졌을 때, 
LOSE panel이 게임 뷰에 잘 나타나는 것으로 봐서는 작 동작할 것으로 예상된다.


Lose panel이 잘 뜨는지 여부 확인완료(콘솔 뷰에도 잘 출력됨을 확인할 수 있다.) / 광고보기 버튼이 잘 뜨는지 확인완료

![image](https://user-images.githubusercontent.com/78609676/125638249-030448fb-6463-4f8c-997d-15719d5d188f.png)


<script src="https://gist.github.com/SeunghyunCho22/aec5bf0b6c2dfa02d38d37585642abb1.js"></script>


다음차시 목표 : 
1. GameManager를 수정하여, 리플레이가 가능하게 만든다. (함정에 떨어졌을때나 게임을 완료했을때)
2. PlayerMove C# Script를 수정하여 점프 문제를 해결한다.
