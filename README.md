# VR 핵심간호술기 - 활력징후 측정

Developed with Unreal Engine 4

<img src="https://user-images.githubusercontent.com/92451281/210622522-cccd7b54-b6f9-48bd-baec-6d220ca730af.png" width="50%" height="50%"><img src="https://user-images.githubusercontent.com/92451281/210622578-05b40ed3-a9c0-4d29-9b78-d26f060a1090.png" width="50%" height="50%"><img src="https://user-images.githubusercontent.com/92451281/210623235-719727c4-c0f7-4ea8-968b-5780c11f2305.png" width="50%" height="50%"><img src="https://user-images.githubusercontent.com/92451281/210622627-49b02977-1b3d-4ddc-92b5-f03b26bc2777.png" width="50%" height="50%"><img src="https://user-images.githubusercontent.com/92451281/210623368-7623bbb4-ab4b-4fe2-b00d-3b2204798df0.png" width="50%" height="50%"><img src="https://user-images.githubusercontent.com/92451281/210622711-19251e30-5fe8-4365-89b4-10a7feeb4c4c.png" width="50%" height="50%"><img src="https://user-images.githubusercontent.com/92451281/210622736-e715480e-01a9-4bc1-8e13-a7a882d9e99b.png" width="50%" height="50%"><img src="https://user-images.githubusercontent.com/92451281/210622783-162eb701-f49b-44b0-bf23-01a0d111b406.png" width="50%" height="50%">

### [시연동영상](https://youtu.be/kEmZCWIJWR0)
---
<핵심간호술기란?>   
한국간호교육평가원에서 제시한 간호사 직무수행 중 빈도와 중요도가 높은 간호술로서 간호사 양성 교육과정 중에 필수적으로 학습되고 성취되어야 할 기술을 의미합니다.

<활력징후 측정>   
핵심기본간호술 평가항목 중 활력징후 측정 컨텐츠를 Unreal Engine 4 로 개발하였습니다.   
Oculus Quest2를 사용하여 VR 컨텐츠로 학습할 수 있습니다.

---
<오류 해결>   

**1. AudioManager 오류 문제 (메시지 로그)**   

버그 현상 : 콘텐츠에서 소리도 나지 않을 뿐만 아니라, 콘텐츠 진행 후 끝내는 동안 메시지 로그에 오류가 많이 쌓이는 현상 발생   
해결 방법 : 퍼시스턴트 레벨로 설정을 한 Start_Content 레벨에 AudioManager를 추가해 줌으로써 해결할 수 있었습니다. (그림 1 참고)   
![image](https://user-images.githubusercontent.com/92451281/213636259-4d60ea97-13e6-404d-a997-9988bf33f81d.png)   
(그림 1)   

**2. 간헐적으로 전자체온계의 뚜껑이 날아다니는 현상**   

버그 현상 : 전자체온계의 뚜껑을 제거하는 부분에서 뚜껑을 제거하게 되면 제거 후 뚜껑이 간헐적으로 날아다니는 현상 발생   
해결 방법 : 전자체온계의 뚜껑제거를 구현하는 부분에서 Bool 변수인 Is Ready To Cap Remove를 True로 설정한 후 제거 될때 Is Ready To Cap Remove를 다시 False로 설정을 해주지 않았기 때문에 오류가 생기게 되었습니다.   
따라서 저는 뚜껑 제거 조건을 모두 만족 시킨 후에 Is Ready To Cap Remove 변수를 False로 설정 해주었습니다. (그림 2 참고)   
![image](https://user-images.githubusercontent.com/92451281/213636674-7c6b47a2-fe65-4df1-a690-96efebca9704.png)   
(그림 2)   

**3. 음성부분 스크립트 잘못 작성**   

버그 현상 : 버그현상은 없지만 딜레이를 사용할 경우 효율이 떨어질 것으로 판단   
해결 방법 : Pawn의 On Speak Success 이벤트 디스패처를 사용하고, Activate Microphone 이벤트를 사용하였습니다. (그림 3 참고)   
![image](https://user-images.githubusercontent.com/92451281/213640592-83f79243-62a8-45d3-99fa-aa9c4eadc47c.png)   
(그림 3)   

**4. 오브젝트들이 TrashCan에 넣어졌을 때 오류 스크립트가 나타나지 않는 현상**  

버그 현상 : 이 콘텐츠에서는 소독솜, 탐침 덮개 만이 폐기될 수 있는 오브젝트인데, 체온계 등을 넣을 때 오류 스크립트가 나타나지 않는 현상   
해결 방법 : TrashCanCollision을 만들어서 StaticMesh에 Polluted라는 이름으로 Component Tag를 추가해 주었습니다.      TrashCanCollision를 추가해주었습니다. (그림 4 참고)   
그리고, Collision 타입을 바꾸는 이벤트를 만들어서 상황에 따라 이벤트를 사용해 주었습니다. (그림 5 참고)   
![image](https://user-images.githubusercontent.com/92451281/213640990-be455d82-1075-4773-8c9a-7926c420db13.png)   
(그림 4)   
![image](https://user-images.githubusercontent.com/92451281/213641003-6eb63d93-5155-45ed-bbb2-034d3eacc6ad.png)   
(그림 5)   

**5. 혈압계 눈금 조절 잘못 구현**   

버그 현상 : 혈압계를 열고 나서 서서히 바늘이 내려가는 것을 구현해야 하는데 잘못 이해하여, 트랙패드를 내리고 있을 때만, 눈금이 내려가게 하였음.   
해결 방법 : 기존의 TrackPad를 통한 눈금을 조절하는 것이 아닌, (그림 6) 과 같이 타임라인으로 이벤트를 만들어, 혈압계 Bulb를 열었을 때, 서서히 눈금이 자동으로 내려가게 구현하였습니다.   
![image](https://user-images.githubusercontent.com/92451281/213641341-8ccad9ef-8db8-4ccc-aea0-2003a563830c.png)   
(그림 6)   

**6. 전자체온계 뚜껑 열기 부분에서 떨어트린 후 ReturnPoint에서의 인터랙션 오류**   

버그 현상 : 전자체온계의 뚜껑을 여는 부분에서 전자체온계를 떨어트리면, ReturnPoint로 돌아오게 되는데, 여기서 전자체온계를 잡으려 하면 전자체온계가 잡히는 것이 아닌 전자체온계의 뚜껑이 열리게 되는 오류   
해결 방법 : 기존에는 전자체온계가 ReturnPoint로 돌아올 때, 처음 전자체온계가 놓여 있던 방향이 아닌 반대 방향으로(뚜껑이 플레이어 쪽을 향함) 놓이게 되었습니다. 또한 기존에 전자체온계의 몸통부분만 인터랙션 할 수 있도록 설정해 놓았기 때문에, 뚜껑이 열리는 현상이 생긴 것 입니다. 따라서 ReturnPoint의 Z 회전을 180도 돌려줌으로써 이러한 문제가 간단하게 해결 되었습니다. (그림 7 참고)   
![image](https://user-images.githubusercontent.com/92451281/213641798-75c15e1a-d081-4008-b5f0-1fd9557f29f1.png)   
(그림 7)   

**7. 혈압계 부분 검지 버튼을 계속 누르면 Cuff가 계속 커지는 현상**   

버그 현상: 검지 버튼을 누르면 혈압계 Cuff 스케일이 커지는 부분에서 160 ~ 200 사이에 이미 도달 했는데도, 검지 버튼을 계속 누르면 Cuff가 계속 커지는 현상   
해결 방법 : 혈압계 Cuff 스케일을 조정하는 이벤트에서 Boolean 변수 IsReadyToCuffScale을 추가형 True 일 때만, 커질 수 있도록 바꾸어 주었습니다. 혈압계 눈금이 160~200에 도달했다면 IsReadyToCuffScale을 False로 변경해주도록 하였습니다.(그림 8 참고)   
![image](https://user-images.githubusercontent.com/92451281/213642191-831d236c-39a6-45b9-91b6-d8d5a99bee7b.png)   
(그림 8)   
