**1. EventStorming Modeling**
---
![image](https://github.com/Old-Temple/assignment_fooddelivery/assets/78444302/da762dea-853c-424e-a615-060220900785)
---

**2. Kafka 설치 후 Sub/Pub 확인**
---
- 클러스터 로드 후 kubectl get all (POD 모두 띄워진 상태 확인)
![K8S_GET_ALL](https://github.com/Old-Temple/assignment_fooddelivery/assets/78444302/4b5478bc-4da1-4222-836c-03a32e274582)
---

---
- 클러스터를 통한 Sub/Pub
  - **front** Micro Service 호출
![sub_pub1](https://github.com/Old-Temple/assignment_fooddelivery/assets/78444302/8e51f85a-6c97-44f5-8ce2-cd2b4113c5dc)
  - **store** Micro Service 호출
![sub_pub2](https://github.com/Old-Temple/assignment_fooddelivery/assets/78444302/7af8911a-8d02-4dab-a4ee-52f30503f312)
  - 위 두 단계에 대한 Kafka Message
![sub_pub3](https://github.com/Old-Temple/assignment_fooddelivery/assets/78444302/22d7f303-58d0-48bd-88eb-b8042ec51912)
---

**3. Server Router 설치**
---
- kubectl get svc
![K8S_GET_SVC](https://github.com/Old-Temple/assignment_fooddelivery/assets/78444302/7fc279f6-1789-4b37-8705-2efef3136f73)
---

**4. Zero downtime Deployment**
---
- new file in front/kubernetes/zerodowntime.yaml (readinessProbe 만 살려둠)
![zerodowntime_2](https://github.com/Old-Temple/assignment_fooddelivery/assets/78444302/98d1f7b5-6c23-4a0a-b0d7-8d2d37de92f8)

- 무중단 확인 (요청 명령어 : siege -c1 -t120S -v http://front:8080/orders --delay=1S)
  - zerodowntime.yaml 파일에서 버전 올리는 거 깜빡하고 한 번 돌려서 front의 v1 레플리카가 두개입니다.
  - gateway도 버전 실수로 v0.1(12stmall), v1.1(배민) 레플리카 두개입니다.
    - 진행은 v1.1로 진행하였습니다.
![zerodowntime_1](https://github.com/Old-Temple/assignment_fooddelivery/assets/78444302/d05168a8-5bc4-4d91-83d4-24f520fc52a3)
---
