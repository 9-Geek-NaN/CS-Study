>**API Gateway**
>
>클라이언트(사용자 또는 애플리케이션)와 백엔드 서비스(서버나 데이터베이스) 사이에서 게이트웨이(관문) 역할을 하는 중요한 컴포넌트


- 쉽게 말해 클라이언트가 API 요청을 보내면 이를 처리하고 적절한 백엔드 서비스로 전달하는 **중간 관리자** 라고 할 수 있음
- API 요청을 수신하고, 트래픽 제한 및 보안 정책을 적용하며 요청을 백엔드 서비스로 전달한 후 클라이언트에게 반환
- API Gateway를 등록해주면, 모든 클라이언트는 각 서비스의 엔드포인트 대신 API Gateway로 요청을 전달하여 관리가 용이해짐
    
    → 사용자가 설정한 라우팅 설정에 따라 각 엔드포인트로 클라이언트를 대리하여 요청하고 응답을 받으면 다시 클라이언트에게 전달하는 **프록시 역할**을 하기 때문
    

## API **Gateway의 주요 역할**

| **역할** | **설명** |
| --- | --- |
| **요청 관리** | 클라이언트 요청을 수신, 분석, 검사 후 백엔드 서비스로 전달 |
| **보안 제공** | • 인증/인가를 통해 요청의 신뢰성을 확인 </br> • 허용/차단 목록(Allow-list/Deny-list) 기능으로 보안을 강화 |
| **트래픽 제어** | 요청 속도 제한(Rate Limiting)으로 서버 과부하 방지 및 시스템 안정성 유지 |
| **프로토콜 변환** | 클라이언트 요청을 백엔드 서비스에서 이해할 수 있는 형태로 변환 |
| **로드 밸런싱** | 여러 요청을 백엔드 서버로 분산하여 시스템 효율성을 높이고 안정성을 보장 |
| **에러 처리** | 류 관리 및 회로 차단(Circuit Breaker) 기능으로 시스템 보호 |
| **모니터링 및 로깅** | API 사용량 및 성능 데이터를 기록, 분석, 시각화하여 관리 효율성 증대 |
| **데이터 캐싱** | 자주 요청되는 데이터를 캐싱해 요청 처리 속도 향상 |

## API Gateway 동작과정

![image](https://github.com/user-attachments/assets/7b0242a9-5ecf-46fc-b843-f3360191c4d8)


**Step 1. 클라이언트 요청** 

클라이언트가 HTTP 요청을 API 게이트웨이로 보냄

**Step 2. 요청 분석 및 검증**

API 게이트웨이는 HTTP 요청의 속성을 분석하고 유효성을 검사

**Step 3. 허용/거부 목록 확인**

허용(allow-list) 및 거부(deny-list) 체크를 수행

**Step 4. 인증 및 권한 확인**

API 게이트웨이는 Identity Provider(아이덴티티 제공자)와 통신하여 요청을 인증 및 권한 확인

**Step 5. 요청 제한 적용**

요청 제한 규칙(rate limiting)을 적용. 초과된 경우 요청을 거부

**Step 6-7. 경로 매칭**

요청이 기본적인 검사를 통과하면 API 게이트웨이는 경로 매칭(Path Matching)을 통해 적절한 서비스를 찾아 요청을 라우팅

**Step 8. 프로토콜 변환**

요청을 적절한 프로토콜로 변환한 뒤 백엔드 마이크로서비스로 전달

**Step 9-12. 에러 처리 및 로깅**

에러를 처리하고 복구가 지연될 경우 `회로 차단(circuit break)`을 적용. 또한 `ELK 스택(Elastic-Logstash-Kibana)`을 통해 `로깅 및 모니터링`을 수행하고, `데이터 캐싱`을 지원하기도 함

## API Gateway를 사용하는 이유

- **보안 강화**: 민감한 데이터에 대한 접근을 중앙에서 통제
- **유연성**: 요청을 여러 서비스로 라우팅하거나 변환할 수 있어 시스템의 유연성이 높아짐
- **확장성**: 요청 트래픽이 많아질 경우 서버 부하를 분산하거나 제한할 수 있음
- **통합 관리**: 모든 API 요청과 응답을 한 곳에서 관리하므로 운영 효율이 향상됨
- **개발자 생산성 향상**: 백엔드 서비스에 대한 직접적인 접근을 막아 개발팀이 각 서비스에만 집중할 수 있음

## 참고

https://github.com/ByteByteGoHq/system-design-101/?tab=readme-ov-file#what-does-api-gateway-do

https://en.wikipedia.org/wiki/API_management

[https://inpa.tistory.com/entry/AWS-📚-API-Gateway-개념-기본-사용법-정리](https://inpa.tistory.com/entry/AWS-%F0%9F%93%9A-API-Gateway-%EA%B0%9C%EB%85%90-%EA%B8%B0%EB%B3%B8-%EC%82%AC%EC%9A%A9%EB%B2%95-%EC%A0%95%EB%A6%AC)
