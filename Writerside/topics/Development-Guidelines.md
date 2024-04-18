# Development Guidelines

개발 지침 정리

## Database
Tool: [Lucid Chart](https://www.lucidchart.com/pages/)

데이터 모델링 과정
: 요구사항 분석 & 개념적 모델링 -> 논리적 & 물리적 모델링 -> 구현 및 검증

1. 요구사항 분석 & 개념적 모델링
   - 클라이언트 측의 요구사항 분석 및 조율
   - 데이터 수집 & 사용 방식 정의 
   - 시스템에 필요한 객체(Entity)와 관계(Relationship) 식별 
   - ERD(Entity Relationship Diagram)를 사용하여 작성 
   - 구체적인 데이터 타입, 길이 등은 고려 x, 데이터의 논리적 구조만 설계
2. 논리적 & 물리적 모델링
   - 각 엔티티에 필요한 속성과 그 타입 정의 
   - 데이터 간 관계 구체화 - 외래키 등의 제약 조건 
   - 테이블, 컬럼, 인덱스 등을 포함한 데이터베이스 스키마 생성 
   - 성능과 공간 최적화를 기술 적용
3. 구현 및 검증
   - 실제 데이터베이스 구축 및 삽입
   - 성능 테스트, 데이터 무결성 및 보안 검증
   - 최적화

네이밍 규칙
1. Schema Name
   - 영어 대문자로 작성
2. Table Name
3. Column Name 
4. Primary Key Name 
5. Foreign Key Name

** 해당 지침은 추후 사용하는 프레임워크나 언어 등에 따라 변경될 수 있습니다.