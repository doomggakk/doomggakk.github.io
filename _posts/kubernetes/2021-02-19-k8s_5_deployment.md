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

### Deployment 생성
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
- 
