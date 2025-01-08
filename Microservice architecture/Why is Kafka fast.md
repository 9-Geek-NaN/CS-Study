# Apache Kafka 완벽 가이드
## 목차
1. Kafka 이해하기
2. Kafka의 핵심 특징
3. Kafka의 구성 요소
4. Kafka의 실제 동작 방식

## 1. Kafka 이해하기
### 1.1 Kafka가 필요한 이유
#### 1.1.1 현대 데이터 처리의 문제점
- 수많은 데이터가 실시간으로 생성되고 있음
    * 사용자의 웹사이트 클릭 로그
    * IoT 센서 데이터
    * 모바일 앱 사용 데이터
    * 결제 시스템 트랜잭션
- 이러한 데이터를 실시간으로 수집하고 처리해야 함
- 여러 시스템 간에 데이터를 안정적으로 주고받아야 함

#### 1.1.2 기존 솔루션의 한계
- 기존 메시징 시스템의 문제점
    * 대용량 데이터 처리 시 성능 저하
    * 데이터 유실 위험
    * 확장이 어려움
- 일반적인 데이터베이스의 한계
    * 실시간 처리의 어려움
    * 높은 비용
    * 시스템 부하 증가

### 1.2 Kafka란?
#### 1.2.1 기본 개념
- 대규모 데이터 스트리밍 플랫폼임
- 마치 우체국처럼 데이터를 중간에서 전달하는 역할을 함
    * 발신자(Producer)가 우체국(Kafka)에 편지(메시지)를 보냄
    * 우체국은 편지를 분류하고 보관함
    * 수신자(Consumer)는 자신의 편지함(Topic)에서 편지를 가져감
- 실시간으로 대량의 데이터를 안전하게 전달할 수 있음

#### 1.2.2 실제 활용 사례
- 넷플릭스: 실시간 추천 시스템 (Kafka를 통해 추천 시스템으로 데이터 전달)
- 우버: 실시간 위치 추적 (운전자의 GPS 위치 정보 수집)
- 라인: 메시지 처리 (사용자 간 메시지 전송)

## 2. Kafka의 핵심 특징
### 2.1 분산 시스템
#### 2.1.1 분산 시스템이란?
- 여러 대의 서버가 하나의 시스템처럼 동작함
- 예시: 한 명의 우체부가 아닌, 여러 명의 우체부가 함께 일하는 것
    * 일부 우체부가 아파도 다른 우체부가 일을 대신함
    * 일이 많아지면 우체부를 더 투입할 수 있음
    * 각 우체부가 특정 구역을 담당하여 효율적으로 일을 처리함

#### 2.1.2 Kafka의 분산 처리 방식
```plaintext
[Producer] --> [Kafka Cluster] --> [Consumer]
                    ↓
      [Broker1] [Broker2] [Broker3]
          ↓         ↓         ↓
       [Data1]   [Data2]   [Data3]
```
- 여러 대의 서버(Broker)가 클러스터를 구성
- 데이터를 분산하여 저장하고 처리
- 서버 장애 시 자동으로 다른 서버가 대체
- 필요에 따라 서버 추가 가능

### 2.2 고성능과 신뢰성
#### 2.2.1 Sequential I/O의 이해
- 하드디스크 접근 방식 비교
    * 랜덤 접근: 집 여러 곳을 왔다갔다하며 물건 찾기
    * 순차 접근: 한쪽 끝에서 다른 쪽 끝까지 차례대로 찾기
- Kafka는 순차 접근 방식을 사용
    * 데이터를 연속적으로 저장
    * 빠른 읽기/쓰기 성능
    * 디스크 효율성 극대화

#### 2.2.2 데이터 복제와 보관
- 데이터 복제 예시
    * 중요한 문서를 여러 장 복사해두는 것과 같음
    * 원본이 손상되어도 복사본으로 복구 가능
```plaintext
[Original Data] --> [Copy 1]
                --> [Copy 2]
                --> [Copy 3]
```
- 안전한 데이터 보관
    * 설정한 기간 동안 데이터 보존
    * 디스크에 안전하게 저장
    * 시스템 장애 시에도 데이터 유실 없음

## 3. Kafka의 구성 요소
### 3.1 Producer (생산자)
#### 3.1.1 Producer의 역할
- 데이터를 생성하고 Kafka로 보내는 주체
- 예시: 실생활의 Producer
    * 쇼핑몰의 주문 시스템
    * 핸드폰의 GPS 센서
    * 웹사이트의 로그 시스템

#### 3.1.2 Producer의 동작 방식
```java
// Producer 예시 코드 (주문 시스템)
Properties props = new Properties();
props.put("bootstrap.servers", "localhost:9092");
props.put("key.serializer", "org.apache.kafka.common.serialization.StringSerializer");
props.put("value.serializer", "org.apache.kafka.common.serialization.StringSerializer");

Producer<String, String> producer = new KafkaProducer<>(props);

// 주문 정보 전송
OrderData order = new OrderData("user123", "product456", 2);
ProducerRecord<String, String> record = 
    new ProducerRecord<>("orders", order.getUserId(), order.toString());
producer.send(record);

// 배송 정보 전송
ShippingData shipping = new ShippingData("order789", "Seoul, Korea");
record = new ProducerRecord<>("shipping", shipping.getOrderId(), shipping.toString());
producer.send(record);
```

### 3.2 Topic (토픽)
#### 3.2.1 Topic의 개념
- 데이터를 구분하는 논리적인 단위
- 실생활 비유
    * 우체국의 우편물 분류함
    * 도서관의 책 분류 시스템
    * 회사의 부서별 문서함

#### 3.2.2 Topic의 구조와 특징
```plaintext
Topic: "orders"
Partition 1: [Message1] -> [Message2] -> [Message3]
Partition 2: [Message4] -> [Message5] -> [Message6]
Partition 3: [Message7] -> [Message8] -> [Message9]

- 각 메시지는 순차적으로 저장
- 파티션으로 분할하여 병렬 처리
- 각 메시지는 고유한 오프셋(위치) 보유
```

### 3.3 Consumer (소비자)
#### 3.3.1 Consumer의 역할
- Topic에서 데이터를 가져와 처리하는 주체
- 실제 사용 예시
    * 주문 데이터 처리 시스템
    * 실시간 대시보드
    * 알림 발송 시스템

#### 3.3.2 Consumer Group
- 여러 Consumer가 협력하여 데이터 처리
- 작동 방식 설명
```plaintext
Topic: "orders"
[Partition 1] --> [Consumer 1]
[Partition 2] --> [Consumer 2]
[Partition 3] --> [Consumer 3]

Consumer Group: "order-processing-group"
- 각 Consumer가 특정 Partition 담당
- 자동 작업 분배
- 장애 시 자동 재분배
```

#### 3.3.3 Consumer 구현 예시
```java
// Consumer 예시 코드 (주문 처리 시스템)
Properties props = new Properties();
props.put("bootstrap.servers", "localhost:9092");
props.put("group.id", "order-processing-group");
props.put("key.deserializer", "org.apache.kafka.common.serialization.StringDeserializer");
props.put("value.deserializer", "org.apache.kafka.common.serialization.StringDeserializer");

KafkaConsumer<String, String> consumer = new KafkaConsumer<>(props);
consumer.subscribe(Arrays.asList("orders"));

while (true) {
    ConsumerRecords<String, String> records = consumer.poll(Duration.ofMillis(100));
    for (ConsumerRecord<String, String> record : records) {
        // 주문 데이터 처리
        OrderData order = OrderData.fromString(record.value());
        processOrder(order);
        
        // 처리 상태 로깅
        System.out.printf("Processed order: %s, amount: %d%n", 
                         order.getUserId(), order.getAmount());
    }
}
```

## 4. Kafka의 실제 동작 방식
### 4.1 메시지 전송 과정
#### 4.1.1 전체 흐름도
```plaintext
[Producer] 
    → [메시지 생성]
    → [Topic 선택]
    → [Partition 결정]
    → [Kafka Cluster]
        → [메시지 저장]
        → [복제본 생성]
    → [Consumer]
        → [메시지 수신]
        → [처리]
```

#### 4.1.2 상세 동작 설명
1. Producer가 메시지 생성
    * 주문 정보, 로그 데이터 등 생성
    * 메시지에 타임스탬프 추가
    * 필요한 경우 메시지 압축

2. Topic과 Partition 선택
    * 메시지 종류에 따라 Topic 결정
    * Partition 선택 방법
        - 라운드 로빈: 균등 분배
        - 키 기반: 동일 키는 동일 Partition
        - 커스텀: 사용자 정의 규칙

3. Kafka Cluster에서의 처리
    * 메시지 수신 및 저장
    * 설정된 수만큼 복제본 생성
    * 저장 완료 확인 응답

4. Consumer의 메시지 처리
    * Poll 방식으로 메시지 가져옴
    * 오프셋 관리로 처리 위치 추적
    * 장애 시 재처리 가능

### 4.2 고가용성 보장
#### 4.2.1 리더와 팔로워
```plaintext
Topic: "orders", Partition 1
[Leader Broker]
    ↓
[Follower 1] [Follower 2]

- Leader: 읽기/쓰기 담당
- Follower: 데이터 복제 및 장애 대비
```

#### 4.2.2 데이터 복제 과정
1. Producer가 Leader에 메시지 전송
2. Leader가 메시지 저장
3. Follower들이 데이터 복제
4. 복제 완료 후 Producer에게 응답

#### 4.2.3 장애 복구 과정
1. Leader 장애 감지
2. 새로운 Leader 선출
3. Producer/Consumer 새 Leader로 연결
4. 정상 동작 재개

### 4.3 데이터 처리 보장
#### 4.3.1 Producer 측면
- 메시지 전송 보장 수준
    * At least once: 최소 한 번 전송 보장
    * At most once: 최대 한 번 전송
    * Exactly once: 정확히 한 번 전송 보장
```java
// Exactly once 설정 예시
props.put("enable.idempotence", true);
props.put("acks", "all");
```

#### 4.3.2 Consumer 측면
- 메시지 처리 보장
    * 오프셋 자동 커밋
    * 수동 커밋으로 정확한 처리 보장
    * 멱등성 있는 처리 구현
```java
// 수동 커밋 예시
consumer.poll(Duration.ofMillis(100));
processMessages(records);
consumer.commitSync(); // 처리 완료 후 커밋
```