###[AWS] AWS ALB vs NLB vs CLB

| <div style="width:200px">Feature</div> | <div style="width:200px">Application Load<br>Balancer</div> | <div style="width:200px">Network Load<br>Balancer</div> | <div style="width:200px">Classic Load <br>Balancer</div> |
| - | :- | :- | :- |
|프로토콜 | HTTP, HTTPS | TCP, UDP, TLS | TCP, SSL/TLS, HTTP, HTTPS|
|플랫폼 | VPC | VPC | EC2-Classic, VPC|
|상태 확인 | ✔ | ✔ | ✔|
|CloudWatch 지표 | ✔ | ✔ | ✔|
|로깅 | ✔ | ✔ | ✔|
|영역 장애 조치 | ✔ | ✔ | ✔|
|Connection Draining(등록 취소 지원) | ✔ | ✔ | ✔|
|같은 인스턴스의 여러 포트로 로드 밸런싱 | ✔ | ✔ |  |
|IP 주소를 대상으로 사용 | ✔ | ✔ (TCP, TLS)  |  |
|로드 밸런서 삭제 탐지 | ✔ | ✔ |  |
|구성 가능한 유휴 연결 시간 초과 | ✔ |   | ✔|
|교차 영역 로드 밸런싱 | ✔ | ✔ | ✔|
|고정 세션 | ✔ |   | ✔|
|정적 IP |   | ✔ |  |
|탄력적 IP 주소 |   | ✔ |  |
|소스 IP 주소 유지 |   | ✔ |  |
|리소스 기반 IAM 권한 | ✔ | ✔ | ✔|
|태그 기반 IAM 권한 | ✔ | ✔ |  |
|느린 시작 | ✔ |   |  |
|WebSocket | ✔ | ✔ |  |
|PrivateLink 지원 |   | ✔ (TCP, TLS)  |  |
|소스 IP 주소 CIDR 기반 라우팅 | ✔ |   |  |
|계층 7|
|경로 기반 라우팅 | ✔ |   |  |
|호스트 기반 라우팅 | ✔ |   |  |
|네이티브 HTTP/2 | ✔ |   |  |
|리디렉션 | ✔ |   |  |
|고정 응답 | ✔ |   |  |
|Lambda 함수를 대상으로 사용 | ✔ |   |  |
|HTTP 헤더 기반 라우팅 | ✔ |   |  |
|HTTP 방법 기반 라우팅 | ✔ |   |  |
|쿼리 문자열 파라미터 기반 라우팅  | ✔ |   |  |
|보안|
|SSL 오프로드 | ✔ | ✔ | ✔|
|SNI(서버 이름 표시) | ✔ | ✔ |  |
|백엔드 서버 암호화 | ✔ | ✔ | ✔|
|사용자 인증 | ✔ |   |  |
|사용자 지정 보안 정책 |   |   | ✔|
| Price (Asia Seoul)<br>checkedAt : 2019-10-01 | 시간당 0.0225 USD<br>LCU-시간당 0.008 USD | 시간당 0.0225 USD<br>LCU-시간당 0.006 USD | 시간당 0.025 USD<br>LCU-시간당 0.008 USD |
