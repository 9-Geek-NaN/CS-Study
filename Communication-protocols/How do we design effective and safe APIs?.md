# 효과적이고 안전한 API를 설계하려면 어떻게 해야 하나요?
## 1. Use clear naming
API의 이름은 자명하고 직관적이어야 합니다!<br>
- /users -> 사용자 정보
- /users/123 -> 특정 사용자 ID에 해당하는 데이터
<br>
<br>

## 2. Ensure reliability through idempotent APIs
idempotence : 동일한 요청을 여러번 반복해도 결과가 변하지않는 API 동작<br>
- GET: 여러 번 호출해도 데이터가 변경되지 않아야 함
- PUT: 동일한 데이터를 업데이트할 경우 결과가 변하지 않아야 함
- DELETE: 리소스 삭제가 요청될 때, 이미 삭제된 경우에도 동일한 응답을 반환해야 함
<br>
<br>

## 3. Add versioning
API 변경사항으로 인해 기존 클라이언트가 영향을 받지않도록 버전관리를 도입해야 합니다!
- /api/v1/carts/123 => /api/v2/carts/123
<br>
<br>

## 4. Add pagination
데이터가 많을 경우 클라이언트가 한번에 모든 데이터를 가져오지 않도록 페이징 기능을 제공해야 합니다!
- 쿼리 매개매개변수를 이용하여 데이터 양을 제한함<br>
ex) GET /users?limit=10&offset=20
- 페이징 정보(총 데이터 수, 현재페이지 등)를 응답에 포함시켜야함
<br>
<br>

## 5. Use clear query strings for sorting and filtering API data\
API 요청 시 클라이언트가 원하는 데이터를 정렬하거나 필터링 할 수 있는 옵션을 제공해야 합니다!<br>
- 필터링 : GET /users?age=30&location-Seoul
- 정렬 : GET /users?sort=age&order=desc
<br>
<br>

## 6. Don't make security an afterthought when designing APIs
보안은 API 설계 후 추가하는 것이 아니라, 설계 초기 단계부터 통합되어야 합니다.
<br>
<br>

## 7. Keep cross-resource references simple
리소스 간 관계를 나타낼 때, 지나치게 복잡한 참조를 피하고 단순하게 설계해야 합니다!
- 가능하면 충첩된 경로 피하기<br>
 /users/123/orders/456/products/789 -> ❌<br>
 /orders/456 -> ⭕️
 <br>
 <br>
 
## 8. Plan for rate limiting
API 요청이 과도하게 발생할 경우 서버의 안정성을 보장하기 위해 요청 제한을 설정합니다.
- IP 주소별 요청 한도를 설정하여 악의적인 요청 차단
