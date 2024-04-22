# Node.js

1. npm init
   package.json 파일 생성 됨
2. npm install --save express
   express 설치
   node_modules 파일 생성 됨
3. npm install --save sequelize
   sequelize 설치
4. sequelize init
   안되면 npx sequelize init

pm2 설치
npm install pm2 -g
-g : 옵션을 주어 전역으로 설치


## Structure
script 작업 시 구조에 대한 고민
controller  
model  
route  
service  
.env  
util

비즈니스 로직과 API 경로를 명확히 분리
route - api 요청에 따른 라우팅  
controller - api 요청/응답에 관한 로직만

MVC
Model, View, Controller  
Model - database 연결  
View - route: 요청을 특정 컨트롤러의 함수로 연결  
Controller - controller: 사용자의 요청을 처리하고 모델을 통해 데이터를 조작한 후 응답을 반환   
service - 데이터 가공. 간단한 데이터 조회 및 업데이트 등에서는 굳이 사용하지 않아도 될듯  
App Entry Point - app.js


Route 분리 기준  
한, 두가지 핵심 기준을 정해서 분리하는게 좋을듯, 규칙이 너무 많아지면 오히려 헷갈림  
1. 리소스 별 분리
2. 기능 별 분리
3. 접근 권한 별 분리
4. 모듈성과 확장성 고려
5. 경로와 메소드 명확성

## Test Process