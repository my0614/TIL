# Kubernetes affinity

## affinity
파드를 원하는 노드에 배치 및 규칙을 설정한다.</br>
Pod 스케줄링에 영향을 주는 정책을 정의하는 필드

## affinity 종류 3가지
- nodeAffinity </br>
Pod 배치할 노드 설정
- podAffinity </br>
특정 Pod가 있는 노드에 배치
- podAntiAffinity </br>
특정 Pod를 비해서 다른 노드에 배치

## nodeAffinity
Pod가 어떤 노드에 올라갈 수 있는지 **라벨 기반 규칙**을 정의한다.</br>
그렇기에 먼저 원하는 노드에 라벨 설정이 되어있는지 먼저 체크가 필요

-> 내가 사용한 방식은 nodeAffinity
```
# 전체 노드 라벨 확인 command
kubectl get nodes --show-labels

# 원하는 노드에 라벨 설정하는 command
kubectl label nodes <노드명> key=value
ex) nodetype = node
```
### nodeAffinity 옵션 2가지
- requiredDuringSchedulingIgnoredDuringExecution</br>
특정 라벨이 있는 노드에 할당하고 싶은 경우에 사용이 된다.
스케줄링 조건이 반드시 충족되어야 하기 때문에 원하는 조건의 노드가 없다면
파드는 스케줄이 되지 않는다.

- preferredDuringSchedulingIgnoredDuringExecution
필수가 아닌 선호되는 요구사항이다.
조건이 충족되지 않더라도 없으면 다른 노드에 할당된다.

## yaml 파일 설정
```
spec:
  affinity:
    nodeAffinity:
      requiredDuringSchedulingIgnoredDuringExecution:
        nodeSelectorTerms:
          - matchExpressions:
              - key: nodetype
                operator: In
                values:
                  - node
```
- nodeSelectorTerms</br>
requiredDuringSchedulingIgnoredDuringExecution에서 사용되는 조건 블록
여러개 사용 가능
- matchExpressions</br>
특정 라벨 조건을 정의하는 부분
이곳에서 아까 노드 라벨 설정했던 라벨 이름을 명시
- key</br>
노드에 붙은 라벨의 key
- operator: In
라벨에 내가 설정한 라벨말고도 여러가지가 있을 수 있기 때문에
내가 설정한 key이 목록중 하나에 포함되면 된다.
- values</br>
노드 라벨의 value값 지정
values를 선택하면 오직 key.value값이 붙은 노드에만 스케줄되도록 지정

