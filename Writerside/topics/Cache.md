# Cache

CDN(Content Delivery Network)   
전 세계 여러 지역에 분산된 서버 네트워크를 사용하여 웹 콘텐츠를 사용자에게 더 빠르게 제공하는 시스템   
웹 사이트의 정적 자원(이미지, 비디오, 자바스크립트 등)을 사용자와 지리적으로 가까운 서버에 캐시하여 저장   

원리
1. 원본 서버 설정: 웹 콘첸츠 원본을 CDN 서비스 제공자와 연결. 중앙 저장소 역할
2. 콘텐츠 복제: CDN 서비스는 원본 서버에서 콘텐츠를 가져와 전 세계의 여러 캐시 서버에 복제
3. 지리적 위치 기반 라우팅: 사용자가 접속하면 위치를 파악하고 가장 가까운 서버로부터 콘텐츠를 제공. DNS 라우팅을 통해 이루어짐
4. 콘텐츠 전달

이점
1. 성능 향상
2. 대역폭 비용 절감: 데이터 전송량이 분산되어 원본 서버의 부하 감소, 전체적인 대역폭 사용량 감소
3. 가용성 및 안정성 증가: 하나의 서버에 문제가 생겨도 다른 서버에서 콘텐츠 제공 가능
4. 보안 강화: DDoS 공격과 같은 네트워크 위협으로부터 보호할 수 있음



쿠키, 세션, 캐시
쿠키 - 클라이언트 쪽에 저장. 클라이언트가 수정, 삭제 등 가능
세션 - 서버 측에 저장. 