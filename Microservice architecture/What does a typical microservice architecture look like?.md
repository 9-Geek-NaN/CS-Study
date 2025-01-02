# What does a typical microservice architecture look like?

![alt text](https://github.com/ByteByteGoHq/system-design-101/blob/main/images/typical-microservice-arch.jpg?raw=true)

## 마이크로서비스 아키텍처의 구성요소
- Load Balancer: 로드 밸런서는 여러 백엔드 서비스로 트래픽을 부산시켜준다.
- CDN(Content Delivery Network): CDN은 정적인 콘텐츠들을 빠르게 전달하기 위해 사용되는 지역적으로 분산되어있는 서버의 그룹을 의미한다. 클라이언트는 컨텐츠를 로딩하기위해 CDN서버에 컨텐츠가 있는지 확인 후 있다면 CDN서버에서 컨텐츠를 가져오고, 없다면 백엔드 서비스에 요청을 한다. CDN서비스에 저장되어 있는 정적 컨텐츠를 가져올 수 있다면 정적 컨텐츠를 빠르게 받아올 수 있다는 장점이 있다.
- API Gateway: API Gateway는 클라이언트의 요청을 처리하고, 관련된 서비스로 라우팅을 해준다. Identify Provider 및 Service Discovery와 통신을 한다.
- Identify Provider: 유저의 인증 및 인가를 다룬다.
- Service Registry & Discovery: 마이크로 서비스의 등록과 검색을 담당하며, API Gateway는 요청을 처리할 관련 서비스를 해당 컴포넌트에서 찾는다.
- Management: 서비스들의 모니터링을 담당한다.
- Microservices: Microservice들은 서로 다른 도메인에서 설계되고, 배포된다. 각각의 도메인은 도메인만의 데이터베이스를 가진다. API Gateway는 REST API 등의 정해진 프로토콜을 사용하여 Microservice들과 통신하고 같은 도메인상에 존재하는 Microservice들은 RPC를 사용하여 통신한다.

## 마이크로서비스의 장점
- 하나의 서비스는 빠르게 설계 및 배포될 수 있으며, 수평적 확장이 가능하다.
- 각각의 도메인은 정해진 팀에의해 독립적으로 유지될 수 있다.
- 비즈니스 요구 사항을 각 도메인에서 맞춤 설정할 수 있기 때문에 더 나은 지원이 가능하다.