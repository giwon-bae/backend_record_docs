# Load Balancing

여러 서버나 컴퓨터 자원에 작업을 고르게 분산하여 처리하는 것. 트래픽이 과도하게 몰려 서비스가 중단되는 일을 막고 지연 없이 작업을 처리

로드 밸런싱의 이점
1. 애플리케이션 가용성
   - 애플리케이션 가동 중지 없이 애플리케이션 서버 유지, 관리 또는 업그레이드 가능
   - 백업 사이트에 자동 재해 복구 제공
   - 상태 확인을 수행하고 가동 중지를 유발할 수 있는 문제 방지
2. 애플리케이션 확장성
   - 한 서버에 트래픽 병목 현상 방지
   - 필요한 경우 다른 서버를 추가하거나 제거할 수 있도록 애플리케이션 트래픽을 예측
   - 안심하고 조정할 수 있도록 시스템에 중복성을 추가 <- 뭔 말인지 잘 모르겠음
3. 애플리케이션 보안
   - 트래픽 모니터링 및 악성 콘텐츠 차단
   - 공격 트래픽을 여러 백엔드 서버로 자동으로 리다이렉션하여 영향 최소화
   - 추가 보안을 위해 네트워크 방화벽 그룹을 통해 트래픽 라우팅
4. 애플리케이션 성능
   - 서버 간에 로드를 균등하게 배포하여 애플리케이션 성능 향상
   - 클라이언트 요청을 지리적으로 더 가까운 서버로 리다이렉션하여 지연 시간 단축
   - 쿨리적 및 가상 컴퓨팅 리소스의 신뢰성 및 성능 보장

* 리다이렉션 : 특정 조건이나 규칙에 따라 들어오는 트래픽을 한 서버나 서비스에서 다른 서버나 서비스로 자동으로 전송하는 과정

로드 밸런싱 알고리즘
1. 정적 로드 밸런싱
   - 라운드 로빈 방식
   - 가중치 기반 라운드 로빈 방식
   - IP 해시 방식
2. 동적 로드 밸런싱
   - 최소 연결 방법
   - 최소 응답 시간 방법

## Load Balancer
로드 밸런서 유형
1. ALB(Application Load Balancer)
   - HTTP와 HTTPS 트래픽에 최적화 되어 있으며, 고급 요청 라우팅 기능을 제공. 애플리케이션 계층 (OSI 모델의 7계층)에서 작동
   - 콘텐츠 기반 라우팅: URL 경로, 호스트 이름, HTTP 헤더, HTTP 메소드 등에 따라 트래픽을 라우팅
   - 호스트 및 경로 기반 라우팅: 다양한 호스트 이름과 URL 경로에 따라 요청을 다른 타겟 그룹으로 라우팅 가능
   - WebSocket 및 HTTP/2 지원: 실시간 통신이 필요한 애플리케이션에 적합
   - 건강 검사: 타겟의 건강 상태를 세밀하게 모니터링하고, 실패한 타겟에서 자동으로 트래픽을 제거
2. NLB(Network Load Balancer)
   - 높은 성능과 초저 지연 시간을 요구하는 TCP, UDP, TLS 트래픽 처리에 적합. 네트워크 계층 (OSI 모델의 4계층)에서 작동
   - 초저 지연 시간: 밀리초 단위의 지연 시간으로 처리 가능
   - 스케일링: 초당 수백만 건의 요청 처리 가능, 자동으로 확장
   - IP 주소를 사용한 라우팅: 소스 및 대상 IP 주소를 기반으로 트래픽을 라우팅
   - 장기 연결 유지: TCP 연결을 장시간 유지할 수 있어 게임 서버 및 IoT 애플리케이션에 적합
3. ELB(Elastic Load Balancer)
   - AWS의 첫 번째 로드 밸런서 유형, 간단한 로드 밸런싱 요구 사항에 적합. 애플리케이션 계층과 네트워크 계층 모두에서 작동 가능
   - 다양한 프로토콜 지원: HTTP, HTTPS, TCP, SSL 프로토콜 지원
   - 간단한 설정: 설정이 비교적 단순, 사용하기 쉬움
   - 건강 검사: 타겟의 건강 상태 체크, 자동으로 트래픽 조정

* 라우팅 : 네트워크에서 데이터 패킷이나 트래픽이 출발점에서 목적지까지 전달되는 경로를 결정하는 과정

## Target Group
로드 밸런서 아래에서 트래픽을 수신할 대상들의 집합

주요 기능
1. 대상 정의: 타겟 그룹은 하나 이상의 대상으로 구성. 이 대상은 EC2 인스턴스, IP 주소, 또는 Lambda 함수 일 수 있으며, 로드 밸런서가 트래픽을 전달할 위치를 정의
2. 건강 검사: 정의된 건강 검사 규칙에 따라서 HTTP 또는 TCP 요청을 통해 주기적으로 상태를 체크. 건강 검사에 실패하면, 그 대상은 트래픽을 수신하지 않음
3. 트래픽 라우팅: 특정 타입의 트래픽을 특정 타겟 그룹에 집중시킬 수 있음

