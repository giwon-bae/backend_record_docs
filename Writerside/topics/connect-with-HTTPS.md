# connect with HTTPS

1. 도메인 구입
2. 도메인 인증
   Route 53 -> 호스팅 영역 생성 -> 도메인 이름 입력 후 생성  
   생성한 호스팅 영역 선택 -> 레코드 생성 -> 값 부분에 IP 주소 입력 후 레코드 생성   
   생성된 NS 주소 4개 가비아에 등록
3. ACM 설정
   인증서 요청 -> 퍼블릭 인증서 요청 -> *.(domain 명)
   인증서 선택 -> Route53에서 레코드 생성  
   2번 과정에서 NS 주소 등록하지 않으면 상태가 검토 중에서 발급됨으로 바뀌지 않음
4. 로드 밸런서를 적용할 Target Group 생성
   EC2 -> Target Group -> Create
   Instances 선택, 타겟명, 포트(api 연결시켜 둔 포트) 설정
   같은 포트 설정 후 Include as pending below -> Create
5. 로드 밸런서
   Application Load Balancer -> 이름 설정, 가용영역 선택(일반적으로 2a, 2c 설정하면 됨), 보안그룹 설정  
   Listeners and routing 설정 : 80, 443, 위에서 설정한 포트(ex. 3000, 8080) -> Target Group 선택 
6. 도메인 설정
   Route 53 -> 호스팅 영역 -> 선택 -> A 유형 레코드 선택 -> 레코드 편집 -> 별칭 on, Application/Classic Load Balancer, 로드 밸런서 선택  
   www 연결 -> 레코드 생성 www 붙이고 위 과정과 동일하게 설정


* https 통신을 위해 로드 밸런서가 꼭 필요한 것은 아님. 다만, 사용하게 되면 보안, 성능, 가용성 및 확장성에 이점이 있음