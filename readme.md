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
