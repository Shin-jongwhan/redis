### 241130
# redis
### <br/><br/><br/>

## docker 환경 구성 방법
### [공식 홈페이지](https://hub.docker.com/_/redis)
### <br/>

### 실행
### 6379는 redis의 기본 포트이다.
### --save는 RDB 스냅샷(Snapshot) 저장 설정을 의미한다. 여러 개 쓸 수 있는데, 60초 안에 1번 이상 변경이 발생하는 경우 스냅샷을 저장한다는 뜻이다.
### --loglevel은 log 저장에 대한 옵션 설정이다.
- debug: 모든 디버깅 정보와 로그를 기록 (가장 상세).
- verbose: 일반 로그 정보, 자세한 이벤트 로그 기록.
- notice: 기본값. 중요 이벤트만 기록.
- warning: 경고와 심각한 오류만 기록 (최소한의 로그).
```
docker run -itd --name redis -v C:\docker_volume\redis:/data -p 6379:6379 redis:alpine3.20 redis-server --save 60 1 --loglevel warning
```
### <br/>

### docker 안으로 접속
```
docker exec -it redis redis-cli
```
### PING이라고 실행해서 PONG이 나오면 잘 연결된 것임.
### 그리고 나갈 때는 quit을 입력한다.
#### ![image](https://github.com/user-attachments/assets/71b975f4-af02-4962-aacd-be4cd43b3e72)
### <br/>

## 잠금(lock)
### 단일 서버를 사용할 때, 여러 서버로 구성하여 노드를 구성할 때 각각 사용하는 잠금 방법이 다르다.
### redis 공식 문서에서는 여러 노드로 구성하면 redlock을 권장한다.
| 특징 | 단일 Redis 잠금 | Redlock (분산 잠금) | 
|---|---|---|
| 사용 환경 | 단일 Redis 인스턴스 | 여러 Redis 인스턴스 (분산 환경) | 
| 신뢰성 | redis 서버 장애 시 신뢰성 약함 | 과반수 노드에서 잠금을 유지 | 
| 네트워크 장애 내성 | 네트워크 장애 시 동기화 어려움 | 노드 일부 장애에도 잠금 유지 | 
| 설정 복잡도 | 간단 | 다수의 Redis 노드와 동기화 필요 | 
### <br/>
