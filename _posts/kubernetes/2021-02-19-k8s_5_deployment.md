---
layout: single
title: 4.Deployment
categories: [Kubernetes]
author_profile: true
---

- Kubernetes의 구성요소인 Deployment에 대해 정리한다

---


## Deployment

### 유스케이스
- ReplicaSet 롤아웃
- 파드의 새로운 상태 선언
- 디플로이먼트의 이전 버전으로 롤백
- 스케일 업
- 일시중지
- 이전 ReplicaSet 정리 등
<br>

## Deployment 생성
```yaml
apiVersion: apps/v1
kind: Deployment # 이부분만 ReplicaSet -> Deployment 수정
metadata:
    name: myapp-replicaset
    labels:
        app: myapp
spec:
    template:
        metadata:
            name: myapp-pod
            labels:
                app: myapp
            spec:
                containers:
                    - name: nginx-container
                      image: nginx
    replicas: 3
    selector: 
        matchLabels:
            app: myapp
```
ReplicaSet의 yaml 파일정의에서 kind만 수정해주면된다.

<br><br>

## RollOut & Versioning
- RollBack ? : 현재 버전에 문제가 발생하여 이전 버전으로 되돌리는 것
- RollOut ? : Release 하는 것을 의미
- RollOut 명령어

```shell
kubectl rollout status deployment/myapp-deployment # rollout 상태 출력
```

```shell
kubectl rollout history deployment/myapp-deployment # rollout 히스토리 출력
```

<br><br>

## Deployment Strategy
1. Recreate : 여러개의 replicas를 업데이트 할 때 이전 것들을 모두 내린 뒤 새로운 것을 띄우는 방식
-> 모든 것을 내린 뒤 새로운 것을 올리는 텀에 사용자가 접속하지 못할 수 있는 안좋은 상황이 발생 할 수 있음
-> 따라서 이 방식은 Deployment의 Default Strategy가 아님

2. Rolling Update : Replica를 하나씩 처리. 한개씩 내리고 올리기를 반복하여 사용자가 접근할 수 없는 문제점을 해소함 
-> Deployment의 Default Strategy임

