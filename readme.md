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
### <br/><br/>

## GUI 툴
### RDM이라는 툴도 있지만 유료라고 하고 나는 redis insight라고 하는 공식 지원 툴을 이용하였다.
#### https://redis.io/insight/
#### ![image](https://github.com/user-attachments/assets/0bf4f358-e8df-4384-8b3e-35a4bb413054)
### <br/><br/>

## TTL (Time To Live)
### 인 메모리 데이터베이스라서 TTL이 중요하다.
### 초 단위로 들어가며, EX로 값을 넣을 수 있다.
```
SET key1 "Hello, Redis" EX 60
```
### <br/><br/>

## Append-Only File (AOF)
### Redis의 모든 쓰기 명령(write commands)을 로그 파일에 기록하는 방식
### 명령어 단위로 데이터를 기록하므로, 서버가 비정상 종료되더라도 AOF 파일을 사용해 데이터를 복구할 수 있다.
- Always
  - 모든 쓰기 명령을 즉시 디스크에 기록.
  - 가장 안전하지만, 성능이 가장 느림.
- Everysec (기본값)
  - 매 초마다 쓰기 명령을 디스크에 기록.
  - 성능과 안정성의 균형.
  - Redis가 비정상 종료되더라도 최대 1초의 데이터만 손실.
- No
  - 운영 체제의 버퍼를 활용해 디스크로 데이터를 플러시.
  - 성능은 좋지만 안정성이 떨어짐.
### <br/><br/>

## RDB (Redis DataBase) 또는 Snapshotting
### RDB는 디스크에 일정 주기로 스냅샷을 따로 저장해놓는 것이다.
### AOF와 같이 복구할 때 쓰는데, 각각 특징이 있다.
| 특징 | AOF | RDB |
|---|---|---|
| 저장 방식 | 명령어 단위로 로그 저장 | 메모리 상태를 특정 시점에 스냅샷 저장 |
| 데이터 손실 가능성 | 최소(최대 1초 손실) | 더 많음 (스냅샷 주기에 따라 다름) |
| 복구 속도 | 느림 | 빠름 |
| 파일 크기 | 더 큼 | 더 작음 |
| 성능 | 상대적으로 느림 | 상대적으로 빠름 |
### <br/><br/>

