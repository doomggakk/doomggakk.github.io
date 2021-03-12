---
layout: single
title: "[CKA Concept] 15. Node Affinity"
categories: [Kubernetes]
author_profile: true
excerpt: CKA 강의 개념 중 쿠버네티스에서의 Node Affinity에 대해 정리한다. 
toc: true
toc_sticky: true
---

## Node Affinity
- Node 유연한 제약조건을 할당하는 기능 (Affinity=유연)

<br>

### Node Affinity 작성방법 
---------------------------
```yaml
apiVersion: 
kind: Pod
metadata:
  name: app-pod
  label:
    app: myapp
spec:
  containers:
    - name: nginx
      image: nginx
  affinity:
    nodeAffinity:
      requiredDuringSchedulingIgnoredDuringExecution:
        nodeSelectorTerms:
        - matchExpressions:
          - key: size
            operator: In
            values:
            - Large
            - Medium

```

- 위의 Affinity는 size = Large or Medium의 조건으로 적용된다.
- operator : ```In```, ```NotIn```, ```Exists```, ```DoesNotExist```, ```Gt```, ```Lt```
- Type of Affinity : <br>
1. ```requiredDuringSchedulingIgnoredDuringExecution``` : Pod가 Node에 스케줄되도록 **반드시** 규칙을 만족해야 하는 것(Node Selector와 같지만 좀 더 표현적인 구문 사용)<br>

    - ex) 인텔 CPU가 있는 Node에만 파드 실행

2. ```preferredDuringSchedulingIgnoredDuringExecution``` : 스케줄러가 시도하려고는 하지만 조건에 맞지 않으면 다른 곳에 스케줄링 한다.<br>

    - ex) 장애 조치영역 XYZ에 Pod를 실행하려하지만 불가능하다면 다른곳에서 일부를 실행하도록 허용

- nodeSelector와 nodeAffinity를 모두 지정한다면 Pod가 후보 Node에 스케줄되기 위해서는 **둘 다 반드시 만족**해야한다.

- nodeSelectorTerms와 연관된 여러 matchExpressions를 지정하면 Pod는 matchExpressions를 **모두 만족**하는 Node에만 스케줄 된다. 

- Pod가 스케줄된 Node의 Label을 지우거나 변경해도 Pod는 제거되지 않는다. Affinity 선택은 **Pod를 스케줄링 하는 시점에만 작동** 한다.




```requiredDuringSchedulingRequiredDuringExecution``` :

<br>
<br>

------------------
**◎ 참고자료**
- Udemy - Certified Kubernetes Administrator (CKA) with Practice Tests

- [쿠버네티스 공식문서 - 노드에 파드 할당하기](https://kubernetes.io/ko/docs/concepts/scheduling-eviction/assign-pod-node/)

