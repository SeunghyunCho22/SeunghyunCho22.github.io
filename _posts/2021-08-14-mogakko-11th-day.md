---
layout: post
title: "[모각코]11th-day"
---

이번 회차에서는 그동안 만들었던 SOL(Shape Of Liberty)게임 속 맵에 구현할 동물들의 움직임 및 전체적인 코드를 정리해서 올려보는 시간을 가졌다.   

using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.AI;

public class Animal : MonoBehaviour
{

    protected StatusController thePlayerStatus;

    [SerializeField] public string animalName; //동물 이름
    [SerializeField] protected int hp; //동물 체력

    [SerializeField]
    private Item item_Prefeb; //아이템
    [SerializeField]
    public int itemNumber; //아이템의 획득 개수

    [SerializeField] protected float walkSpeed; // 걷기 속도
    [SerializeField] protected float runSpeed; //뛰기 속도

    protected Vector3 destination; //방향

    //상태변수
    protected bool isAction; //행동 중인지 아닌지 판별
    protected bool isWalking; //걷는 중인지 아닌지 판별
    protected bool isRunning; //뛰는지 판별
    protected bool isChasing; //추격중인지 판별
    protected bool isAttacking; //공격중인지 판별
    public bool isDead; //죽었는지 판별

    [SerializeField] protected float walkTime; //걷기 시간
    [SerializeField] protected float waitTime; //대기 시간
    [SerializeField] protected float runTime; //뛰기 시간

    protected float currentTime;

    //필요한 컴포넌트
    [SerializeField] protected Animator anim;
    [SerializeField] protected Rigidbody rigid;
    [SerializeField] protected BoxCollider boxCol;
    protected AudioSource theAudio;
    protected NavMeshAgent nav;
    protected FieldOfViewAngle theViewAngle;

    [SerializeField] protected AudioClip[] sound_Normal;
    [SerializeField] protected AudioClip sound_Hurt;
    [SerializeField] protected AudioClip sound_Dead;

    [SerializeField] protected bool isSpecialAction = false;
    [SerializeField] protected float specialacttime;
    // Start is called before the first frame update
    void Start()
    {
        thePlayerStatus = FindObjectOfType<StatusController>();
        theViewAngle = GetComponent<FieldOfViewAngle>();
        nav = GetComponent<NavMeshAgent>();
        theAudio = GetComponent<AudioSource>();
        currentTime = waitTime;
        isAction = true;
    }

    // Update is called once per frame
    protected virtual void Update()
    {
        if (!isDead)
        {
            Move();
            ElapseTime();
        }
    }

    protected void Move()
    {
        if ((isWalking || isRunning) && !isSpecialAction)
        {
            //rigid.MovePosition(transform.position + (transform.forward * applySpeed * Time.deltaTime));
            nav.SetDestination(transform.position + destination * 5f);
            
        }
        
    }

    protected void ElapseTime()
    {
        if (isAction)
        {
            currentTime -= Time.deltaTime;
            if (currentTime <= 0 && !isChasing && !isAttacking)
            {
                ReSet();
            }
        }
    }

    protected virtual void ReSet()
    {
        isWalking = false;
        isAction = true;
        nav.speed = walkSpeed;
        isRunning = false;
        nav.ResetPath();
        anim.SetBool("Walking", isWalking);
        anim.SetBool("Running", isRunning);
        // destination.Set(Random.Range(-0.2f, 0.2f), 0f, Random.Range(0.5f, 1f));
        destination.Set(Random.Range(-1f, 1f), 0f, Random.Range(-1f, 1f));
    }

    protected void TryWalk()
    {
        isWalking = true;
        anim.SetBool("Walking", isWalking);
        currentTime = walkTime;
        nav.speed = walkSpeed;
        Debug.Log("걷기");
    }

    public virtual void Damage(int _dmg, Vector3 _targetPos)
    {
        if (!isDead)
        {
            hp -= _dmg;

            if (hp <= 0)
            {
                Dead();
                return;
            }

            PlaySE(sound_Hurt);
            anim.SetTrigger("Hurt");
        }
        //hp -= _dmg;

        //if (hp <= 0)
        //{
        //    Debug.Log("체력 0 이하");
        //    return;
        //}

        //PlaySE(sound_Hurt);
        //anim.SetTrigger("Hurt");
    }

    protected void Dead()
    {
        PlaySE(sound_Dead);
        isWalking = false;
        isRunning = false;
        isChasing = false;
        isAttacking = false;
        isDead = true;
        nav.ResetPath();
        StopAllCoroutines();
        anim.SetTrigger("Dead");
    }

    protected void RandomSound()
    {
        int _random = Random.Range(0, sound_Normal.Length); //일상 사운드 3개
        PlaySE(sound_Normal[_random]);
    }

    protected void PlaySE(AudioClip _clip)
    {
        theAudio.clip = _clip;
        theAudio.Play();
    }

    public Item GetItem()
    {
        this.gameObject.tag = "Untagged";
        Destroy(this.gameObject, 3f);
        return item_Prefeb;
    }
}
   

위의 코드는 StrongAnimal과 WeakAnimal에게 상속해줄 수 있는 Animal 코드의 완성본이다.   
제작된 위의 코드를 이용하여, Strong_Wolf(늑대/육식동물)과 Weak_Deer(사슴/초식동물)의 수정된 코드는 아래와 같다.   
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Strong_Wolf : StrongAnimal
{
    [SerializeField] protected int[] rate;
    protected override void Update()
    {
        base.Update();
        if (theViewAngle.View() && !isDead && !isAttacking && !isSpecialAction)
        {
            StopAllCoroutines();
            StartCoroutine(ChaseTargetCoroutine());
        }
    }

    protected override void ReSet()
    {
        base.ReSet();
        RandomAction();
    }

    private void RandomAction()
    {
        RandomSound();
        int _random = Random.Range(0, rate.Length); //대기, 하울링, 걷기

        if (0<=_random&& 2>_random)
        //    Wait();
              TryWalk();

        else if (2==_random )
            //  Howling();
            TryWalk();
        else if (3<=_random && _random<rate.Length)
            //TryWalk();
            StartCoroutine(Howling());
    }

    private void Wait()
    {
        currentTime = waitTime;
        Debug.Log("대기");
    }
    private IEnumerator Howling()
    {
        currentTime = waitTime;
        isSpecialAction = true;
        anim.SetTrigger("Howling");
        Debug.Log("하울링");
        yield return new WaitForSeconds(specialacttime);
        isSpecialAction = false;

    }
}
   
이는 육식동물 - Strong_Wolf이다.   

using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.Scripting.APIUpdating;

public class Weak_deer : WeakAnimal
{
    protected override void Update()
    {
        base.Update();
        if (theViewAngle.View() && !isDead)
        {
            Run(theViewAngle.GetTargetPos());
        }
    }

    protected override void ReSet()
    {
        base.ReSet();
        RandomAction();
    }

    private void RandomAction()
    {
        RandomSound();

        int _random = Random.Range(0, 4); //대기, 풀뜯기,걷기

        if (_random == 0)
            Wait();
        else if (_random == 1)
            Eat();
        else if (_random == 2)
            TryWalk();
    }

    private void Wait()
    {
        currentTime = waitTime;
        Debug.Log("대기");
    }
    private void Eat()
    {
        currentTime = waitTime;
        anim.SetTrigger("Eat");
        Debug.Log("풀뜯기");
    }
}
   
이는 초식동물 - Weak_Deer이다.   
다음 차시에서는 위의 동물을 인게임 내에서 구현해보고 움직임을 확인해보고 애니메이터를 추가/수정 해보는 시간을 가져보겠다.
