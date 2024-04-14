# HTTP

HTTP(HyperText Transfer Protocol) : 웹에서 정보를 교환하는데 사용되는 핵심 프로토콜
웹 브라우저와 웹 서버 간의 통신을 가능하게 하며, 웹의 구조적 기초를 이루고 있음

특징
1. 비연결성: 클라이언트
2. 무상태성
3. 확장 가능성

요청(Request) 구성 요소
1. 메소드(Method): 클라이언트가 수행하고자 하는 작업의 유형
2. URI(Uniform Resource Identifier): 요청 대상이 되는 자원의 위치
3. HTTP 버전: 사용하는 HTTP 프로토콜의 버전 (ex. HTTP/1.1, HTTP/2)
4. 헤더(Headers): 요청에 대한 추가 정보를 포함 (ex. Content-Type 헤더: 본문 유형, Authorization 헤더: 인증 정보 제공)
5. 바디(Body)(선택): POST나 PUT 같은 메소드에서 데이터를 전송할 때 사용. 데이터 형식은 헤더의 Content-Type에 따라서 결정

메소드
1. GET: 자원 검색 시 사용
2. POST: 자원 생성할 때 사용
3. PUT: 자원 업데이트 시 사용
4. DELETE: 자원 삭제 시 사용
5. HEAD: GET과 유사하지만, 바디 없이 헤더 정보만 요청할 때 사용
6. OPTIONS: 대상 리소스에 대한 통신 옵션을 조회할 때 사용

응답(Response) 구성 요소
1. 상태 코드(Status Code): 요청의 성공 여부 
2. HTTP 버전
3. 헤더(Headers): 응답과 관련된 추가 정보 포함 (ex. Content-Length: 응답 바디의 길이)
4. 바디(Body)(선택): 실제 요청된 데이터를 포함

상태 코드
1. 1xx(정보 응답)
   1) 100 Continue: 클라이언트가 나머지 요청을 계속 보낼 수 있음을 알림
   2) 101 Switching Protocols: 서버가 클라이언트의 프로토콜 전환 요청을 수락했음을 나타냄
2. 2xx(성공)
   1) 200 OK: 요청이 성공적으로 처리됨
   2) 201 Created: 요청이 성공적으로 처리되어 새로운 리소스가 생성됨
   3) 204 No Content: 요청은 성공적이지만 서버가 보낼 콘텐츠가 없음
3. 3xx(리다이렉션)
   1) 301 Moved Permanently: 요청한 리소스가 영구적으로 새 위치로 이동 되었음
   2) 302 Found: 요청한 리소스가 일시적으로 다른 위치로 이동 되었음
   3) 304 Not Modified: 클라이언트가 조건부 GET 요청을 보냈고 리소스가 수정되지 않았다면, 이 응답을 사용할 수 있음
4. 4xx(클라이언트 오류)
   1) 400 Bad Request: 서버가 요청을 이해하지 못함. 일반적으로 요청 구문 오류
   2) 401 Unauthorized: 요청이 인증을 요구하나 클라이언트가 그것을 제공하지 않음
   3) 403 Forbidden: 서버가 요청을 이해했으나 접근을 거부함
   4) 404 Not Found: 서버가 요청한 리소스를 찾을 수 없음
   5) 429 Too Many Requests: 클라이언트가 일정 시간 동안 너무 많은 요청을 보냈음을 나타냄
5. 5xx(서버 오류)
   1) 500 Internal Server Error: 서버에 오류가 발생하여 요청을 수행할 수 없음
   2) 501 Not Implemented: 서버가 요청 메소드를 지원하지 않아 요청을 수행할 수 없음
   3) 503 Service Unavailable: 서버가 일시적으로 요청을 처리할 수 없음. 주로 서버 오버로드나 유지보수로 인해 발생
   4) 504 Gateway Timeout: 서버가 게이트웨이나 프록시 역할을 하며, 상위 서버로부터 시간 내에 응답을 받지 못함