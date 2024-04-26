# AWS + Firebase

## 전체적인 로직

## 이메일 + 패스워드
1. 클라이언트 측에서 회원가입 API 호출
   - ID/PW를 입력받고 해당 ID/PW를 body에 포함시켜 회원가입 api 호출
2. 서버 측 유저 생성
   - api를 통해 받아온 ID/PW와 Firebase Auth의 createUser를 이용하여 유저 생성
   - 생성된 유저의 uid를 이용하여 user 테이블에 필드값 추가
   - 필요에 따라 admin.auth().setCustomUserClaims를 이용하여 권한 설정
   - 성공/실패에 따른 결과값 반환 
3. 클라이언트 측 로그인
   - 회원가입 api 호출 결과 성공 시 ID/PW를 이용하여 Firebase Auth에 로그인
4. Firebase Auth 측 검증
   - ID/PW를 통해 검증 후 ID 토큰 반환
5. 로그인 성공
   - 로그인 성공 시 클라이언트 측 화면은 다음 화면(ex. main 화면)으로 넘어가게 됨
   - 로그인 성공 시 발급받은 토큰을 이용해서 추가적인 API 호출 가능

## 소셜 로그인
약간의 수정이 조금 더 필요할듯?
OAuth 이용
1. 소셜 로그인 버튼 클릭
   - 클라이언트 애플리케이션은 사용자를 소셜 OAuth 서버로 리디렉션
   - 이 때, 필요한 정보(리디렉션 URI, 클라이언트 ID, 스코프, 응답 유형 등)를 요청 URL에 포함
2. 소셜 로그인 페이지에서 인증
   - 사용자는 소셜 로그인 페이지에서 자신의 계정 정보로 로그인
   - 이 과정에서 필요한 권한(ex. 프로필 정보 접근)을 부여
3. 애플리케이션으로 리디렉션
   - 사용자를 클라이언트로 리디렉션하며 'authorization code'를 URL에 포함시켜 전달
4. Authorization Code로 Access Token 요청
   - 클라이언트는 받은 'authorization code'를 사용하여 소셜 인증 서버에 'access token'을 요청
   - *Kakao Login은 3번 과정을 내부적으로 처리
5. Access Token을 통한 사용자 인증
   - 소셜 인증 서버는 요청을 검증한 후에 'access token'과 'refresh token'을 클라이언트에 발급
   - 클라이언트는 발급 받은 'access token'을 이용하여 Firebase Auth에 로그인을 요청
6. 로그인 완료 및 사용자 인터페이스로 복귀
   - Firebase에서 사용자 인증이 완료되면, 클라이언트는 사용자를 애플리케이션의 로그인 후 페이지로 리디렉션