# Redis 사용법!

## Redis Type
1. String
2. Hash
3. List
4. Set
5. Sorted Set(ZSet)
6. Bitmap

> 다음과 같은 타입도 있긴 하다!   
> HyperLogLog, Geospatial, Streams, JSON, Bloom Filter, Time Series

## 1. String 타입
가장 기본적인 데이터 타입으로, 텍스트나 바이너리 데이터를 저장

### 사용 시기
- 단순 키-값 저장
- 캐싱
- 카운터
- 세션 데이터

### 특징
- 최대 512MB까지 저장 가능
- 바이너리 안전(Binary-safe)
- 숫자도 문자열로 저장하여 증감 연산 가능

### 주요 명령어
```redis
# 기본 문자열 조작
SET key "value"                    # 값 설정
GET key                           # 값 조회
DEL key                          # 키 삭제
EXISTS key                       # 키 존재 여부 확인

# 만료시간 설정
SET key "value" EX 3600          # 3600초 후 만료
TTL key                         # 남은 만료 시간 확인

# 다중 키 연산
MSET key1 "value1" key2 "value2" # 여러 키 동시 설정
MGET key1 key2                  # 여러 키 동시 조회

# 숫자 연산
SET counter 0                    # 카운터 초기화
INCR counter                    # 1 증가
INCRBY counter 5                # 5 증가
DECR counter                    # 1 감소
DECRBY counter 5                # 5 감소

# 부분 문자열 조작
APPEND key "addition"           # 문자열 뒤에 추가
GETRANGE key 0 3               # 부분 문자열 조회
SETRANGE key 0 "new"           # 부분 문자열 변경
STRLEN key                     # 문자열 길이 조회
```

## 2. Hash 타입
키-값 쌍을 저장하는 해시 맵 구조

### 사용 시기
- 객체 데이터 저장
- 필드별 갱신이 필요한 경우
- 부분 데이터 조회가 필요한 경우


### 특징
- 객체 구조 표현에 적합
- 메모리 효율적
- 개별 필드 접근 가능

### 주요 명령어
```redis
# 기본 해시 조작
HSET user:123 name "John" age 30  # 필드 설정
HGET user:123 name               # 단일 필드 조회
HMGET user:123 name age         # 다중 필드 조회
HGETALL user:123                # 모든 필드-값 조회
HDEL user:123 age              # 필드 삭제

# 필드 존재 여부
HEXISTS user:123 name          # 필드 존재 확인

# 숫자 연산
HINCRBY user:123 points 10     # 숫자 필드 증가
HINCRBYFLOAT user:123 score 1.5 # 실수 필드 증가

# 필드 조회
HKEYS user:123                 # 모든 필드명 조회
HVALS user:123                 # 모든 값 조회
HLEN user:123                  # 필드 개수 조회

# 조건부 설정
HSETNX user:123 email "john@example.com" # 필드가 없을 때만 설정
```

## 3. List 타입
문자열을 양방향 연결 리스트로 저장하는 데이터 타입

### 사용 시기
- 최근 데이터 관리 (최근 게시물, 로그)
- 메시지 큐 구현
- 순서가 중요한 데이터

### 특징
- 양방향 푸시/팝 연산 지원
- 인덱스 기반 접근 가능
- 큐와 스택 구현에 적합

### 주요 명령어
```redis
# 기본 리스트 조작
LPUSH mylist "first"           # 왼쪽에 추가
RPUSH mylist "last"            # 오른쪽에 추가
LPOP mylist                    # 왼쪽에서 제거
RPOP mylist                    # 오른쪽에서 제거

# 리스트 조회
LRANGE mylist 0 -1            # 전체 리스트 조회
LLEN mylist                   # 리스트 길이 조회
LINDEX mylist 1               # 특정 인덱스 조회

# 리스트 수정
LSET mylist 1 "new value"     # 특정 인덱스 값 변경
LTRIM mylist 0 9              # 리스트 자르기 (0~9 유지)

# 블로킹 연산
BLPOP mylist 5                # 왼쪽 팝 (5초 대기)
BRPOP mylist 5                # 오른쪽 팝 (5초 대기)

# 리스트 간 이동
RPOPLPUSH source dest         # source에서 팝하여 dest로 푸시
```

## 4. Set 타입
정렬되지 않은 문자열의 집합

### 사용 시기
- 유니크한 데이터 관리
- 태그 시스템
- 친구/팔로워 관계

### 특징
- 중복 값 불허
- 빠른 멤버십 테스트
- 집합 연산 지원

### 주요 명령어
```redis
# 기본 집합 조작
SADD myset "member1"          # 멤버 추가
SREM myset "member1"          # 멤버 제거
SMEMBERS myset               # 모든 멤버 조회
SCARD myset                  # 멤버 수 조회

# 멤버십 테스트
SISMEMBER myset "member1"    # 멤버 존재 여부 확인

# 집합 연산
SUNION set1 set2            # 합집합
SINTER set1 set2            # 교집합
SDIFF set1 set2             # 차집합

# 랜덤 조작
SPOP myset                  # 랜덤 멤버 제거 및 반환
SRANDMEMBER myset          # 랜덤 멤버 조회

# 집합 연산 결과 저장
SUNIONSTORE dest set1 set2  # 합집합 결과 저장
SINTERSTORE dest set1 set2  # 교집합 결과 저장
SDIFFSTORE dest set1 set2   # 차집합 결과 저장
```

## 5. Sorted Set (ZSet) 타입
점수를 기준으로 정렬된 문자열 집합

### 사용 시기
- 순위 시스템
- 점수 기반 정렬
- 범위 검색이 필요한 경우

### 특징
- 모든 요소가 점수와 연관됨
- 점수 기반 자동 정렬
- 범위 기반 연산 지원

### 주요 명령어
```redis
# 기본 정렬 집합 조작
ZADD leaderboard 100 "user1"   # 멤버와 점수 추가
ZSCORE leaderboard "user1"    # 점수 조회
ZRANK leaderboard "user1"     # 순위 조회 (오름차순)
ZREVRANK leaderboard "user1"  # 순위 조회 (내림차순)

# 범위 조회
ZRANGE leaderboard 0 -1 WITHSCORES       # 전체 조회 (오름차순)
ZREVRANGE leaderboard 0 -1 WITHSCORES    # 전체 조회 (내림차순)
ZRANGEBYSCORE leaderboard 80 100         # 점수 범위 조회

# 집합 수정
ZINCRBY leaderboard 10 "user1"   # 점수 증가
ZREM leaderboard "user1"         # 멤버 제거
ZREMRANGEBYRANK leaderboard 0 1  # 순위 범위 제거
ZREMRANGEBYSCORE leaderboard 0 80 # 점수 범위 제거

# 집합 정보
ZCARD leaderboard               # 멤버 수 조회
ZCOUNT leaderboard 80 100      # 점수 범위 내 멤버 수
```

## 6. Bitmap 타입
비트 단위의 연산을 지원하는 특수한 String 타입

### 사용 시기
- 사용자 활동 로그
- 실시간 분석

### 특징
- 메모리 효율적 (1비트/플래그)
- 비트 연산 지원
- 최대 2^32 비트 저장 가능

### 주요 명령어
```redis
# 기본 비트맵 조작
SETBIT bitmap 100 1           # 특정 위치 비트 설정
GETBIT bitmap 100            # 특정 위치 비트 조회
BITCOUNT bitmap              # 1인 비트 개수 조회
BITPOS bitmap 1 0            # 첫 1 비트 위치 조회

# 비트 연산
BITOP AND result bitmap1 bitmap2  # AND 연산
BITOP OR result bitmap1 bitmap2   # OR 연산
BITOP XOR result bitmap1 bitmap2  # XOR 연산
BITOP NOT result bitmap          # NOT 연산

# 범위 연산
BITCOUNT bitmap 0 1         # 특정 바이트 범위의 1 비트 수
BITFIELD bitmap GET u4 0    # 4비트 부호 없는 정수로 조회
```

<br><br><br>

출처  
https://redis.io/docs/latest/develop/data-types/  
https://github.com/ByteByteGoHq/system-design-101?tab=readme-ov-file#how-can-redis-be-used