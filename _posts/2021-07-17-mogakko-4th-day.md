---
layout: post
title: "[모각코]4th-day"
---

4th Mogakko.

Mission : 
1. GameManager를 수정하여, 리플레이 기능을 활성화한다.
2. PlayerMove C# Script에 점프기능을 추가하여 구현한다. 

이전 시간에 해결하지 못했던 점프기능을 추가하였다.

![image](https://user-images.githubusercontent.com/78609676/126075451-c5fe9dd1-77d0-48f0-9539-b37763aaa117.png)

스페이스바를 누르면 점프가 구현되게 하였다.

   void Update()
      {
          //Jump
          if (Input.GetButtonDown("Jump") && !anim.GetBool("isJump"))
          {
              rigid.AddForce(Vector2.up * jumpPower, ForceMode2D.Impulse);
              anim.SetBool("isJump", true);
          }
          //Stop Speed
          if (Input.GetButtonUp("Horizontal"))
          {
              rigid.velocity = new Vector2(rigid.velocity.normalized.x * 0.5f, rigid.velocity.y);
          }

          //Direction Sprite
          if (Input.GetButton("Horizontal"))
              spriteRenderer.flipX = Input.GetAxisRaw("Horizontal") == -1;

          //Animation
          if (Mathf.Abs(rigid.velocity.x) < 0.3)
              anim.SetBool("isWalk", false);
          else
              anim.SetBool("isWalk", true);
      }
      
      
또한 저번 시간에 목표했던 GameManager에서 replay를 구현하여, lose나 win panel이 떴을때 화면을 클릭하면 replay가 되게 구현하였다.

<script src="https://gist.github.com/SeunghyunCho22/c24a78f292300c6830083e9d826f5f15.js"></script>

다음차시 목표:
오르막길(마찰력 등) 물리엔진 구현
