# gRPC는 어떻게 작동하나요?

gRPC는 구글에서 만든 RPC프레임워크입니다.

RPC는 Remote Procedure Call 의 약자로 프로세스 간 통신의 한 형태.<br>
이름 그대로 네트워크로 연결된 서버 상의 프로시저(함수, 메서드 등)를 원격으로 호출할 수 있는 기능입니다.<br>
한 마디로 분산되어있는 컴퓨터간의 통신을 위한기술!(MSA에서 많이 씀)
<br>
<br>
## RPC의 핵심 : Stub
RPC의 매커니즘

![img_4](https://github.com/user-attachments/assets/1d28b269-f9af-4e9c-aa77-495bd27fb70e)<br>
 reference: https://www.guru99.com/ko/remote-procedure-call-rpc.html

스텁: 매개변수(parameter)객체를 메세지로 변환/역변환 하는 레이어

클라이언트 스텁 : 함수 호출에서 사용된 파라미터의 변환 및 함수 실행 후 서버에 전달된 결과를 변환하는 담당<br>
서버 스텁 : 클라이언트가 전달한 매개 변수의 역변환 및 함수 실행 결과 변환을 담당
<br>
<br>

## gRPC의 특징
- Protocol Buffer : Serialization 하여 데이터를 전달<br>
데이터 구조를 .proto 파일에 정의하여 통신<br>
메세지 키만 간소화하는것이 아니라 직렬화 하여 전송<br>
(REST는 Serialization없이 Json, XML을 사용 -> 상대적으로 용량이 크다!)
![img_2 (1)](https://github.com/user-attachments/assets/6aa55212-8f3a-40b7-be56-6e51055384ca)<br>
reference: https://martin.kleppmann.com/2012/12/05/schema-evolution-in-avro-protocol-buffers-thrift.html<br>
<br>
<br>

- HTTP2를 사용하여 Multiplexing 사용가능!
REST는 HTTP1.1을 사용
<br>
<br>
## gRPC 예제
.proto 확장자 파일<br>

![397024341-b0f7ea5a-44e9-4b8b-bda0-e6188d47eedf](https://github.com/user-attachments/assets/45c28c01-740e-4ae3-a9cb-e5253706f358)<br>
- 각 메시지가 어떻게 작성될지에 관한 약속으로 서버와 클라이언트 모두에게 공유됨
- 이를 기준으로 서버와 클라이언트는 서로 주고받는 메세지를 작성,해독 함
서버(파이썬)와 클라이언트(자바) 코드

![397025650-238392f7-6769-4dc8-944b-f5f09d7a2bc9](https://github.com/user-attachments/assets/105304c2-a11a-4500-b584-8581c00ee192)<br>
- .proto파일에 있던 CheckBookAvailability가 서버에서 함수로 정의되어있고
이를 클라이언트에서 stub 객체를 통해 호출하는 것을 볼 수 있다
<br>
<br>
예제 reference: https://www.youtube.com/watch?v=uwrR5e5_FH8
<br>
## 그렇다면 무조건 RPC를 쓰는게 좋은가?
아니다!<br>
보내는 데이터가 작을때는 REST가 더 효율적이다
![img_1](https://github.com/user-attachments/assets/ec90de92-20d0-47e2-a809-08a356a83cc3)
reference: https://medium.com/@i.gorton/scaling-up-rest-versus-grpc-benchmark-tests-551f73ed88d4

# 참고
<br>

### REST와의 차이점
---
| **특징**         | **gRPC**                                          | **REST**                               |
|------------------|-------------------------------------------------|---------------------------------------|
| **전송 프로토콜** | HTTP/2                                           | HTTP/1.1                              |
| **데이터 형식**   | Protocol Buffers (바이너리)                      | JSON (텍스트)                         |
| **성능**         | 빠름 (바이너리 전송, 스트리밍 지원)                | 상대적으로 느림 (JSON 직렬화/역직렬화) |
| **스트리밍**      | 클라이언트 및 서버 양방향 스트리밍 지원           | 제한적 (서버 푸시 기반)                |
| **언어 지원**     | 다수의 언어를 위한 코드 생성                     | 언어 독립적 (HTTP 클라이언트로 구현 가능) |
<br>

<br>

### gRPC VS HTTP API
---
| **특성**          | **gRPC**                     | **HTTP API**            |
|-------------------|-----------------------------|-------------------------|
| **계약**          | `.proto` 파일 생성 필수       | 실행을 위한 파일 불필요  |
| **프로토콜**       | HTTP 2.0                    | HTTP                    |
| **Payload**       | Protobuf                    | JSON, Text              |
| **스트리밍**       | Client, Server, 양방향        | Client, Server          |
| **브라우저 지원**   | 미지원                      | 지원                    |
| **보안**          | TLS                         | TLS                     |
