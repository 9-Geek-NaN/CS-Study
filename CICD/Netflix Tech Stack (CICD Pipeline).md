![image](https://github.com/user-attachments/assets/d5414bc3-8835-4c8c-a350-664cf3badad2)
![image](https://github.com/user-attachments/assets/b80d6015-8028-439e-a6c1-6d43a7453ac7)

## **1. 계획(Planning)**

- JIRA를 사용해 계획을 세우고, Confluence를 사용해 문서를 작성
- **JIRA**:
    - 소프트웨어 개발을 위한 애자일 프로젝트 관리 도구
    - 기능: 작업 추적, 스프린트 계획, 이슈 관리
- **Confluence**:
    - 팀의 협업과 문서화를 위한 도구
    - 기능: 팀 간 지식 공유, 프로젝트 문서 관리, 기술 문서 작성
    

## **2. 코딩(Coding)**

- 백엔드 서비스 주요 언어로 Java를 사용하며, 용도에 따라 Python, Node.js, Scala 등 다양한 언어를 추가로 사용

## **3. 빌드(Build)**

- Gradle을 주로 빌드 도구로 사용하며, 다양한 사용 사례를 지원하기 위해 Gradle 플러그인을 개발함
- **Gradle**:
    - 고성능과 유연성을 가진 오픈 소스 빌드 도구로, 빌드 속도와 확장성을 제공

## **4. 패키징(Packaging)**

- 패키지와 종속성은 아마존 머신 이미지(AMI)에 포함되어 릴리스됨
- **Amazon Machine Image (AMI):**
    - AWS에서 제공하는 가상 머신 이미지로, 애플리케이션과 종속성을 포함하여 일관된 환경을 제공
    

## **5. 테스트(Testing)**

- 넷플릭스의 프로덕션 중심 문화에 맞게 Chaos 도구를 강조한 테스트가 진행됨
- **Chaos Engineering**:
    - 의도적으로 **혼란(Chaos)**를 주입해 시스템의 **복원력**과 **안정성**을 검증하고 향상시키는 접근 방식
    - Netflix가 설계한 Chaos Monkey, Chaos Kong 등 혼란 주입 도구를 통해 시스템 복원력 검증
    - 목적: 장애 발생 시 시스템의 신뢰성을 테스트하고, 프로덕션 환경에서의 문제를 사전에 발견

## **6. 배포(Deployment)**

- 넷플릭스는 자체적으로 구축한 Spinnaker를 사용해 카나리 롤아웃 방식으로 배포를 진행
- **카나리 롤아웃 배포**: 카나리 배포와 롤아웃 배포를 결합한 방식으로, 새로운 버전을 점진적으로 배포하며 동시에 각 단계에서 안정성을 평가
    - 새 버전을 일부 서버에 배포하고 안정성을 평가한 후 안정적이면 배포를 확장
- **Spinnaker**:
    - 넷플릭스와 구글이 공동 개발
    - 멀티 클라우드 환경을 지원하는 오픈 소스 지속적 배포 도구
    - 카나리 배포 및 단계적 배포를 통해 서비스 중단 최소화

## **7. 모니터링(Monitoring)**

- 모니터링 지표는 Atlas에 중앙 집중화 되며,  케이엔타(Kayenta)를 사용하여 이상(anomaly)을 감지
- **Atlas**:
    - Netflix가 개발한 내부 모니터링 도구로 실시간 메트릭 수집 및 시각화 지원
- **Kayenta**:
    - Netflix의 카나리 분석 도구로, 새로운 버전이 기존 버전보다 안정적인지 판단

## **8. 사건 보고(Incident report)**

- 사건은 우선순위에 따라 처리되며, PagerDuty를 통해 사건을 처리
- **PagerDuty**:
    - 사건 발생 시 알림을 전송하고 우선순위에 따라 적절한 대응 팀 호출
 
## 참고
https://github.com/ByteByteGoHq/system-design-101/?tab=readme-ov-file#cicd
