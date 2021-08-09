---
layout: post
title: "[모각코]9th-day"
---

8월 7일 회차에서는 오픈월드 서바이벌 게임의 유닛에 해당하는 동물들(초식동물, 육식동물, 잡식동물) 대부분을 제작해보고, 각 동물의 스크립트와 animator를 손봤다.
player가 동물을 공격하여 정해진 hp를 감소시켜 hp가 0에 도달시키면 동물이 death하는데, 이때 동물에게 접근하면,   

![image](https://user-images.githubusercontent.com/78609676/128658466-27604000-e253-4737-ac6a-0b035bec9c68.png)


위 사진과 같이 "[animal이름] 해체하기 (E)" 라는 문구가 뜨며, E를 누르면 player가 해체하는 모션(칼을 사용) 을 하며 기존의 설정해두었던 고기가 동물이 해체된 자리에 놓여진다.

![image](https://user-images.githubusercontent.com/78609676/128658556-9d67871d-ab32-462e-b1e9-08f4b9be8d78.png)

       
       
위와 같이 동물에 해당하는 제작된 스크립트를 보면 Item_Prefeb칸에서 Meat_Raw(날고기), Meat_Cooked(익힌고기), Meat_Burnt(탄 고기)중 해체 위치에 놓일 고기를 설정해줄 수 있다.
※참고로 익히지 않은 날 고기를 습득할 시, player의 행복도가 감소함.※
