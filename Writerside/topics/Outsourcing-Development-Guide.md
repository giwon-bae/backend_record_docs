# Outsourcing Development Guide

클라이언트 측 준비 사항
1. AWS 계정, 인스턴스 유형 선택 (미 선택시, 프리티어 사용 - 추후 변경 가능)
2. IAM 설정 - 문서 참조
3. 도메인 - 가비아에서 구입, https 통신을 위함
4. 각 뷰에 사용되는 데이터 정의가 완료된 기획서 - DB 구조 설계를 위함

기본 셋팅 작업 순서   
1. ec2 인스턴스 생성 및 접속
2. 시스템 패키지를 최신 상태로 유지하기 위한 명령어 입력
   ```
   sudo apt update
   sudo apt upgrade -y
   ```
3. 필요한 소프트웨어 설치 (nodejs)
   ```
   nvm 설치 : curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
   로드 : source ~/.bashrc
   최신 LTS 버전의 Node.js 설치 : nvm install --lts
   테스트 : node -e "console.log('Running Node.js ' + process.version)" 
   ```
   <a href="https://github.com/nvm-sh/nvm/blob/master/README.md " ignore-vars="true">nvm 버전 확인</a>
4. 데이터베이스 설치
   설치
   ```
   sudo apt-get update
   sudo apt-get install mysql-server
   ```
   버전 확인
   ```
   mysql --version
   ```
   mysql 기본 보안 설정
   ```
   sudo mysql_secure_installation
   ```
   VALIDATE PASSWORD COMPONENT - 비밀번호 검증 기능   
   Y : 비밀번호 검증 기능 활성화. 정해진 기준에 따른 강력한 비밀번호를 설정하도록 유도. 정해진 기준에 따르지 않으면 MySQL에서 거부   
   N : 비밀번호 검증 기능 비활성화.   
   LOW    Length >= 8
   MEDIUM Length >= 8, numeric, mixed case, and special characters
   STRONG Length >= 8, numeric, mixed case, special characters and dictionary
   Remove anonymous users? - 익명 유저 제거   
   Y : 익명 사용자 제거. 보안 강화   
   N : 익명 사용자를 제거하지 않음. 사용자 계정이 설정되지 않은 상태에서도 누구나 MySQL에 로그인할 수 있게 됨   
   Disallow root login remotely? - root 사용자의 원격 접속 차단   
   Y : root 사용자가 로컬 컴퓨터에서만 MySQL에 접근할 수 있도록 설정   
   N : root 사용자가 원격에서도 로그인 할 수 있도록 허용   
   Remove test database and access to it? - test 데이터베이스 제거   
   Y : test 데이터베이스와 그에 대한 접근 권한 제거   
   N : 제거하지 않음   
   Reload privilege tables now? - 권한 테이블 리로드   
   Y : 권한 테이블 리로드. 모든 설정 변경 사항이 적용되도록 함   
   N : 리로드하지 않음. 변경 사항이 적용되지 않음

   mysql 접근
   ```
   sudo mysql -u root
   ```
   암호 설정 - 암호 설정 없이 종료 시 찾을 수 없음
   ```
   {} 내부에 있는 내용은 {} 없이 직접 넣어줘야 함
   데이터베이스 생성
   CREATE DATABASE {DB명}
   사용자 생성 및 권한 부여
   CREATE USER '{user}'@'{localhost}' IDENTIFIED BY '{password}';
   GRANT ALL PRIVILEGES ON {DB명}.* TO '{user}'@'{localhost}';
   변경사항 적용
   FLUSH PRIVILEGES;
   ```
   외부 접속 허용하기 (mysqld.cnf) 수정
   ec2에서 최고 권한 부여받기
   ```
   sudo su
   ```
   mysqld.cnf 디렉토리로 이동 및 파일 실행
   ```
   cd /etc/mysql/mysql.conf.d
   vi mysqld.cnf
   ```
   bind-address 수정하기
   ```
   bind-address = 0.0.0.0
   ```
5. 로컬 작업 환경 셋팅
   5.1 WebStorm
      1. New Project -> Empty Project 생성
      2. Tools ->  Deployment -> Configuration -> SSH configuration 옆의 점 3개 클릭
      3. Host(IP 주소), Username(일반적으로 ubuntu) 작성 후 Key pair를 통한 인증
      4. Root path Autodetect, 로컬 파일과 서버 파일 Mapping (폴더명을 일치 시켜줘야하는 듯함)
      5. Tools -> Deployment -> Options -> Upload changed files automatically to the default server 설정   
         Skip external change : 원격 서버에서 다른 사람이나 다른 프로세스에 의해 파일이 수정되었을 때, 이러한 변경사항을 무시하고 로컬에서의 변경사항만을 서버로 업로드   
         Delete remote files when local are deleted : 로컬 서버에서 파일 삭제 시 원격 서버에서도 삭제
   
   5.2 DataGrip
      1. New Project 생성
      2. Database Explorer -> New -> Data Source -> MySQL
      3. Host(IP 주소 입력), User, Password 입력 후 Test Connection
      4. schema 생성
6. 초기화 설정
   npm init - package name, version 등을 설정하고 초기화
   npm i express - express 설치