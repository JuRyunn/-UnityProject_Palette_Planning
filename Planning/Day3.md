## 사용할만한 asset들
- [캐릭터 모션: 1](https://assetstore.unity.com/packages/3d/animations/free-32-rpg-animations-215058)
- [캐릭터 모션: 2](https://assetstore.unity.com/packages/3d/animations/rpg-character-mecanim-animation-pack-free-65284)
- [캐릭터 모션: 3](https://assetstore.unity.com/packages/3d/animations/warrior-pack-bundle-2-free-42454)
- [몹: 고블린](https://assetstore.unity.com/packages/3d/characters/humanoids/fantasy/mini-legion-grunt-pbr-hp-polyart-98187)
- [몹: 곰](https://assetstore.unity.com/packages/3d/characters/animals/free-stylized-bear-forest-animal-228910)

<br>

## 참고할 영상
- [조이스틱으로 움직임 제어](https://www.youtube.com/watch?v=GGqwMGZiwCg)
- [3D 모델 구하기, 리깅 방법](https://www.youtube.com/watch?v=oFBGs4_jJ0Y&t=620s)
- [카메라 제어](https://www.youtube.com/watch?v=4611qmBWTC0)
- [목표 추적 AI 만들기](https://www.youtube.com/watch?v=FBY_cmtCNHw)

<br>

## 코드
#### 유저 캐릭터 제어 코드
```C#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class PlayerMovement : MonoBehaviour
{
    public VariableJoystick joystick;
    public float speed;

    Rigidbody rigid;
    Animator anim;
    Vector3 moveVec;

    void Awake()
    {
        rigid = GetComponent<Rigidbody>();
        anim = GetComponent<Animator>();
    }

    private void FixedUpdate()
    {
        float x = joystick.Horizontal;
        float z = joystick.Vertical;

        moveVec = new Vector3(x, 0, z) * speed * Time.deltaTime;
        rigid.MovePosition(rigid.position + moveVec);

        if (moveVec.sqrMagnitude == 0)
            return;

        Quaternion dirQuat = Quaternion.LookRotation(moveVec);
        Quaternion moveQuat = Quaternion.Slerp(rigid.rotation, dirQuat, 0.3f);
        rigid.MoveRotation(moveQuat);
                

    }
}

```

#### 유저 추적 카메라 코드
```C#
using System.Collections;
using UnityEngine;

public class FollowCam : MonoBehaviour{
    public Transform target;
    public float dist = 10.0f;
    public float height = 5.0f;
    public float smoothRotate = 5.0f;

    private Transform tr;
        
    void Start (){
        tr = GetComponent<Transform> ();

    }

    void LateUpdate () {

        float currYAngle = Mathf.LerpAngle (tr.eulerAngles.y, target.eulerAngles.y,smoothRotate *Time.deltaTime);

        Quaternion rot = Quaternion.Euler (0, currYAngle, 0);

        tr.position = target.position - (rot * Vector3.forward * dist) + (Vector3.up*height);

        tr.LookAt (target);

    }
    
}
```
