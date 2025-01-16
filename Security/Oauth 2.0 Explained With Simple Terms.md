OAuth 2.0 간단히 설명하기
  
> OAuth 2.0은 서로 다른 애플리케이션이 민감한 자격 증명을 공유하지 않고도 사용자를 대신하여 상호 작용할 수 있도록 하는 강력하고 안전한 보안 프레임워크이다.
![alt text](https://github.com/ByteByteGoHq/system-design-101/blob/main/images/oAuth2.jpg?raw=true)

## OAuth의 핵심 개념
> OAuth의 핵심 개념은 사용자, 서버 그리고 IDP(Identity Provider)이다.
  
## OAuth의 실행 단계
1. 사용자가 IDP에 로그인 정보를 보낸다.
2. IDP는 사용자에게 Authorization Code를 보낸다.
3. 사용자가 Authorization Code와 함께 데이터를 요청한다.
3. 서버는 IDP에 유효한 Authorization Code인지를 물어보고 유효하다면 Access Token을 얻는다.
4. 서버는 Access 토큰을 이용해 사용자의 정보를 받아온다.
  
## OAuth 토큰의 역할
OAuth를 사용하여 얻을 수 있는 OAuth 토큰은 다음과 같은 작업을 수행할 수 있다.
- 단일 로그인(SSO): OAuth 토큰을 사용하여 한 번의 로그인으로 여러 서비스 혹은 앱에 로그인할 수 있다.(Ex. 대학 홈페이지, Google 로그인 등)
- 시스템 전반에 걸친 권한 부여: OAuth 토큰을 사용하면 다양한 시스템에서 액세스 권한을 공유할 수 있기 때문에 모든 곳에서 별도로 로그인할 필요가 없다.
- 사용자 프로필 액세스: OAuth 토큰이 있는 앱은 사용자 프로필의 특정 데이터에 액세스할 수 있다. 하지만 모든 정보를 볼 순 없기 때문에 보안적으로 걱정할 필요는 없다.