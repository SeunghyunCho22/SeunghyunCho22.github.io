---
layout: post
title: "[모각코]7th-day"
---

7월 31일 회차에서는 기존에 진행하고 있던 오픈월드 서바이벌 게임의 유닛들(animals)를 제작하는 시간을 가졌다.

![image](https://user-images.githubusercontent.com/78609676/127775135-4720ccc3-94b8-40f5-831e-54dbb8c3a166.png)

우선 동물 제작에 앞서 엑셀로 유니티 asset store에서 구매했던,
![image](https://user-images.githubusercontent.com/78609676/127775403-218ee6f8-ee9a-4a2d-915d-371fd525031f.png)
Low Poly Animated Animals, Low Poly Animated Dinosaurs, Low Poly Animated Prehistoric Animals

그리고 이번에 새로 구매한

![image](https://user-images.githubusercontent.com/78609676/127775478-f3fa5170-5a25-47bd-ac3f-b1cd13caa8d6.png)

Animal pack deluxe v2의 디폴트 값 및 직접 입력한 물리값들을 엑셀파일로 정리했다.

그리고 직접 제작 과정에 들어갔는데, 
![image](https://user-images.githubusercontent.com/78609676/127775510-f6a7bfe4-4c53-4772-a793-b878fefcc401.png)

![image](https://user-images.githubusercontent.com/78609676/127775525-9439abd5-7a3d-4230-a22b-5ac1d0a741ff.png)

현재 Low Poly에 해당하는 동물들 중 초식동물(herbivores)은 6마리를 제작하였고, 육식동물(predators)은 3마리,
Animal pack deluxe v2의 실사 동물들은 초식동물 3마리, 욱식동물 2마리를 제작하였다.

간단하게만 설명을 하자면, 육식동물은 Player을 발견하면 공격을 하기 위해 다가오고, 초식동물은 Player을 발견하면 도망을 간다.
이는 각각 육식동물에 해당하는 동물은 StrongAnimal을 상속받고, 초식동물에 해당하는 동물은 WeakAnimal을 상속받는다. 또한 StrongAnimal과 WeakAnimal은
Animal이라는 상위 스크립트로부터 상속받는다.

StrongAnimal에서 Wolf를, WeakAnimal에서 Deer스크립트를 보면,

<script src="https://gist.github.com/SeunghyunCho22/8bc0d99b188836dd69086cd14c96fc4a.js"></script>

<script src="https://gist.github.com/SeunghyunCho22/2b1081f527a0fe8ecb67d064ca50be25.js"></script>

이다.
