---
layout: post
title: "[모각코]2nd-day"
---

2nd Mogakko.

Mission : Allowing up to two jumps. / Inserting background sound & jumping sound.

처음에 더블점프까지 허용하기 위하여 c# script에 jumpCount라는 새로운 변수를 할당한 후 충돌 시(ground 등등..) jumpCount를 0으로 초기화하는 방법을 사용하려 하였으나,
현재 어떤 이유에서인지 실행이 잘 되지 않음. ※추후 수정 예정.


![image](https://user-images.githubusercontent.com/78609676/125198452-dfa77000-e29c-11eb-8490-47ed6a1ebd01.png)


Complete inserting background sound & jumping sound!

c# script

  using System;
  using System.Collections;
  using System.Collections.Generic;
  using System.Collections.Specialized;
  using UnityEngine;

  public class Character : MonoBehaviour
  {
      private Rigidbody2D rigid;
      public int jumpCount = 0;
      float bounce = 5f;

      public AudioSource mySfx;

      public AudioClip jumpSfx;

      SpriteRenderer spriteRenderer;

      Animator anim;

      GameObject character;

      void Start()
      {
          rigid = GetComponent<Rigidbody2D>();
          spriteRenderer = GetComponent<SpriteRenderer>();
          anim = GetComponent<Animator>();
          this.character = GameObject.Find("character");
      }



      void OncollisionEnter2D(Collider2D col)
      {
          jumpCount = 0;
          if (col.gameObject.tag == "groundunit")
          {
              Debug.Log("충돌");
          }
      }



      void Update()
      {
          float hor = Input.GetAxisRaw("Horizontal");

          rigid.velocity = new Vector2(hor * 3.0f, rigid.velocity.y);

          if (jumpCount < 2)
          {

              if (Input.GetKeyDown(KeyCode.W))
              {
                  anim.SetBool("isJumping", true);
                  rigid.AddForce(Vector2.up * bounce, ForceMode2D.Impulse);
                  jumpCount++;
                  JumpSound();

              }

              else
              {
                  anim.SetBool("isJumping", false);
              }

          }

          if (Input.GetKeyDown(KeyCode.DownArrow))
          {
              anim.SetBool("isSliding", true);

          }
          else if (Input.GetKeyUp(KeyCode.DownArrow))
          {
              anim.SetBool("isSliding", false);
          }


          //방향상태
          if (Input.GetButtonDown("Horizontal"))
          {
              spriteRenderer.flipX = Input.GetAxisRaw("Horizontal") == -1;
          }

          //animation walk
          if (rigid.velocity.normalized.x == 0)
          {
              anim.SetBool("isWalking", false);
          }
          else
          {
              anim.SetBool("isWalking", true);
          }


      }

      void JumpSound()
      {
          mySfx.PlayOneShot(jumpSfx);
      }
  }
