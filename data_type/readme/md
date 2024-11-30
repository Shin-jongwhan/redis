
# Redis 데이터 타입 정리

Redis는 다양한 데이터 타입을 지원하여 다양한 데이터를 저장하고 처리할 수 있습니다. 각 데이터 타입과 주요 명령어 및 사용 예제를 아래에 정리했습니다.

---

## 1. Strings
- **가장 기본적인 데이터 타입.**
- 하나의 키에 최대 512MB 크기의 문자열 데이터를 저장.
- 숫자 데이터를 저장하면 간단한 계산(증가/감소)도 가능.

### 주요 명령어
- `SET key value`: 문자열 값 저장.
- `GET key`: 문자열 값 가져오기.
- `INCR key`: 숫자 값을 1 증가.
- `DECR key`: 숫자 값을 1 감소.
- `APPEND key value`: 문자열에 값을 추가.

### 예제
```bash
SET key1 "Hello, Redis"
GET key1
> "Hello, Redis"

INCR counter
GET counter
> "1"
```

---

## 2. Lists
- **순서를 유지하는 연결 리스트.**
- 요소를 앞쪽(`LPUSH`) 또는 뒤쪽(`RPUSH`)에 추가 가능.
- FIFO(First In First Out) 큐나 LIFO(Last In First Out) 스택 구현 가능.

### 주요 명령어
- `LPUSH key value`: 리스트 앞쪽에 요소 추가.
- `RPUSH key value`: 리스트 뒤쪽에 요소 추가.
- `LRANGE key start stop`: 특정 범위의 리스트 요소 가져오기.
- `LPOP key`: 리스트의 첫 번째 요소 제거.
- `RPOP key`: 리스트의 마지막 요소 제거.

### 예제
```bash
LPUSH mylist "A"
RPUSH mylist "B"
LRANGE mylist 0 -1
> ["A", "B"]

LPOP mylist
> "A"
```

---

## 3. Sets
- **중복 없는 집합 데이터.**
- 순서가 없는 데이터 저장에 적합.
- 합집합, 교집합, 차집합 같은 집합 연산 지원.

### 주요 명령어
- `SADD key value`: 집합에 값 추가.
- `SMEMBERS key`: 집합의 모든 요소 가져오기.
- `SISMEMBER key value`: 값이 집합에 포함되어 있는지 확인.
- `SUNION key1 key2`: 두 집합의 합집합.
- `SINTER key1 key2`: 두 집합의 교집합.

### 예제
```bash
SADD myset "one"
SADD myset "two"
SMEMBERS myset
> ["one", "two"]

SISMEMBER myset "one"
> 1
```

---

## 4. Sorted Sets (Zsets)
- **점수(score)를 기반으로 정렬된 집합 데이터.**
- 요소와 함께 숫자 점수를 저장하여 자동으로 정렬.

### 주요 명령어
- `ZADD key score value`: 정렬된 집합에 요소 추가.
- `ZRANGE key start stop`: 특정 범위의 요소 가져오기.
- `ZRANGEBYSCORE key min max`: 점수 범위 내 요소 가져오기.
- `ZREM key value`: 특정 요소 제거.

### 예제
```bash
ZADD leaderboard 100 "Player1"
ZADD leaderboard 200 "Player2"
ZRANGE leaderboard 0 -1 WITHSCORES
> ["Player1", 100, "Player2", 200]
```

---

## 5. Hashes
- **필드와 값을 저장하는 데이터 타입.**
- 관계형 데이터베이스의 행(row)과 비슷한 구조.

### 주요 명령어
- `HSET key field value`: 필드에 값 설정.
- `HGET key field`: 특정 필드 값 가져오기.
- `HGETALL key`: 모든 필드와 값 가져오기.
- `HDEL key field`: 특정 필드 삭제.

### 예제
```bash
HSET user:1 name "Alice"
HSET user:1 age "30"
HGET user:1 name
> "Alice"

HGETALL user:1
> ["name", "Alice", "age", "30"]
```

---

## 6. Streams
- **로그와 같은 시간 순서 데이터 저장.**
- 실시간 데이터 처리에 적합하며, 메시지 큐 역할 수행.

### 주요 명령어
- `XADD key * field value`: 스트림에 데이터 추가.
- `XRANGE key start end`: 특정 범위의 스트림 데이터 가져오기.
- `XREAD COUNT count STREAMS key ID`: 특정 스트림 읽기.

### 예제
```bash
XADD mystream * sensor_id "1234" temperature "22.5"
XRANGE mystream - +
> ["sensor_id", "1234", "temperature", "22.5"]
```

---

## 7. HyperLogLog
- **중복된 데이터가 있는 대규모 데이터의 고유 값 개수 추정.**
- 저장 공간을 크게 절약하면서 데이터 개수를 추정.

### 주요 명령어
- `PFADD key value`: 요소 추가.
- `PFCOUNT key`: 고유 값 개수 추정.

### 예제
```bash
PFADD visitors "user1"
PFADD visitors "user2"
PFCOUNT visitors
> 2
```

---

## 8. Geospatial Indexes
- **위도와 경도 데이터 저장 및 검색.**
- 특정 거리 안의 위치 검색 등에 유용.

### 주요 명령어
- `GEOADD key longitude latitude member`: 위치 데이터 추가.
- `GEORADIUS key longitude latitude radius unit`: 특정 거리 내의 위치 검색.

### 예제
```bash
GEOADD cities 13.361389 38.115556 "Palermo"
GEOADD cities 15.087269 37.502669 "Catania"
GEORADIUS cities 15 37 200 km
> ["Catania"]
```

---

## 9. Bitmaps
- **비트 단위의 데이터 처리.**
- 효율적으로 비트 연산과 집계를 수행.

### 주요 명령어
- `SETBIT key offset value`: 특정 비트 설정.
- `GETBIT key offset`: 특정 비트 값 가져오기.
- `BITCOUNT key`: 비트 값 1의 개수 세기.

### 예제
```bash
SETBIT mykey 7 1
GETBIT mykey 7
> 1

BITCOUNT mykey
> 1
```

---

## 요약
Redis 데이터 타입은 다음과 같습니다:
1. **Strings**: 기본 문자열 데이터.
2. **Lists**: 순서를 유지하는 리스트.
3. **Sets**: 중복 없는 집합.
4. **Sorted Sets (Zsets)**: 점수 기반 정렬 집합.
5. **Hashes**: 필드-값 쌍.
6. **Streams**: 시간 순서 로그 데이터.
7. **HyperLogLog**: 고유 값 개수 추정.
8. **Geospatial Indexes**: 위치 데이터.
9. **Bitmaps**: 비트 연산.

각 데이터 타입은 다양한 사용 사례를 지원합니다.
