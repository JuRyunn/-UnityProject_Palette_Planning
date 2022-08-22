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
- [카메라 제어]()
- [목표 추적 AI 만들기](https://www.youtube.com/watch?v=FBY_cmtCNHw)


## 코드 (확실하지 않음)
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

// 스크립트 창에서 추적할 오브젝트 선택



```
