## 몬스터가 플레이어 추적: 1
- [참고영상: 1](https://www.youtube.com/watch?v=3_5RBUGpdH8&t=353s)
#### Code
```C#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class MonsterMovement : MonoBehaviour
{
    Animator GoblinAni;

    public Transform target; // 쫒아갈 타겟
    public float GoblinSpeed;
    bool enableAct; // 액션스위치
    int atkStep; // 공격단계

    private void Start()
    {
        GoblinAni = GetComponent<Animator>();
        enableAct = true;
    }

    
    void RotateGoblin() // 몬스터가 타겟을 바라보게하는 코드
    {
        Vector3 dir = target.position - transform.position;

        transform.localRotation =
            Quaternion.Slerp(transform.localRotation,
                Quaternion.LookRotation(dir), 5 * Time.deltaTime);
    }

    void MoveGoblin() // 몬스터가 타겟을 향해 이동하는 코드
    {
        // 타겟과의 거리가 10이상일 경우 이동
        if((target.position - transform.position).magnitude >= 10)
        {
            GoblinAni.SetBool("Walk", true);
            transform.Translate(Vector3.forward * GoblinSpeed * Time.deltaTime, Space.Self);
        }

        // 10이하일 경우 정지
        if((target.position - transform.position).magnitude < 10)
        {
            GoblinAni.SetBool("Walk", false);
        }
    }

    private void Update()
    {
        if (enableAct)
        {
            // 기능 실행
            RotateGoblin();
            MoveGoblin();
        }
    }

    void GoblinAtk() // 공격 기능 코드
    {
        // 거리가 10 이하일 경우
        if((target.position - transform.position).magnitude < 10)
        {
            // 두가지 공격 패턴
            switch (atkStep)
            {
                case 0:
                    atkStep += 1;
                    GoblinAni.Play("Attack 01");
                    break;

                case 1:
                    atkStep += 1;
                    GoblinAni.Play("Attack 02");
                    break;
            }
        }
    }

    // 공격 모션중엔 이동, 회젼 x 
    void FreezeGoblin()
    {
        enableAct = false;
    }
    void UnFreezeGoblin()
    {
        enableAct = true;
    }
}
```
#### Animator
![image](https://user-images.githubusercontent.com/79950504/186148621-79d569f6-412d-4879-ab69-93c68b0f5b57.png)


<br>

## 몬스터가 플레이어 추적: 2
- [참고영상: 2](https://www.youtube.com/watch?v=UvDqnbjEEak)

#### Windows -> AI -> Navigation -> Bake -> clear -> bake
![image](https://user-images.githubusercontent.com/79950504/186148964-3df18308-bbc3-4b10-bfc0-a679574b4e3c.png)


