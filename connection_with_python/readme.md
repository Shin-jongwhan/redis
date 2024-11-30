### 241130
## python에서 redis 연결하는 방법
### redis 설치
```
pip install redis
```
### <br/>

### redis_manager.py
```
import redis

class common : 
	def __init__(self) : 
		pass


	def connection(self) : 
		# Redis 클라이언트 생성
		client = redis.StrictRedis(host='127.0.0.1', port=6379)

		# PING 테스트
		response = client.ping()
		print("Connected to Redis:", response)  # 출력: Connected to Redis: True

		# 데이터 저장 및 조회
		client.set("key", "value")
		value = client.get("key").decode("utf-8")
		print("Value for 'key':", value)  # 출력: Value for 'key': value
```
### <br/>

### 접속 테스트
#### ![image](https://github.com/user-attachments/assets/7fd71278-f33c-4369-a94a-c3311bb5f1c8)
