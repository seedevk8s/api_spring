# React Reply API 프로젝트 구조 분석

## 📁 전체 프로젝트 구조

```
api_spring/
├── 📁 src/
│   ├── 📁 main/
│   │   ├── 📁 java/react/reply/
│   │   │   ├── 📄 ReactReplyApplication.java (메인 애플리케이션)
│   │   │   ├── 📁 security/ (보안 관련 - 10개 파일)
│   │   │   ├── 📁 reply/ (게시글 관련 - 3개 파일)
│   │   │   ├── 📁 comment/ (댓글 관련 - 3개 파일)
│   │   │   ├── 📁 user/ (사용자 관련 - 1개 파일)
│   │   │   └── 📁 util/ (유틸리티 - 3개 파일)
│   │   └── 📁 resources/
│   │       └── 📄 application.properties (설정 파일)
│   └── 📁 test/
│       └── 📁 java/react/reply/
│           ├── 📄 ReactReplyApplicationTests.java
│           ├── 📄 ReplyTest.java
│           └── 📁 security/
│               └── 📄 JwtTest.java
├── 📄 build.gradle (빌드 설정)
├── 📄 react_reply.sql (데이터베이스 스키마)
└── 📁 postman_export/ (API 테스트 컬렉션)
```

## 🏗️ 아키텍처 패턴

**계층형 아키텍처 (Layered Architecture)**를 따르고 있습니다:

```
┌─────────────────────────────────────┐
│           Presentation Layer        │
│  ┌─────────────┐ ┌─────────────┐   │
│  │ReplyController│ │CommentController│   │
│  └─────────────┘ └─────────────┘   │
└─────────────────────────────────────┘
┌─────────────────────────────────────┐
│           Business Layer            │
│  ┌─────────────┐ ┌─────────────┐   │
│  │ReplyRepository│ │CommentRepository│   │
│  └─────────────┘ └─────────────┘   │
└─────────────────────────────────────┘
┌─────────────────────────────────────┐
│           Data Layer                │
│  ┌─────────────┐ ┌─────────────┐   │
│  │ReplyEntity  │ │CommentEntity│   │
│  └─────────────┘ └─────────────┘   │
└─────────────────────────────────────┘
```

## 📦 패키지별 상세 구조

### 1. Security 패키지 (10개 파일)
```
security/
├── SecurityConfig.java          # Spring Security 설정
├── JWTUtil.java                 # JWT 토큰 생성/검증
├── ApiLoginFilter.java          # 로그인 인증 필터
├── TokenCheckFilter.java        # 토큰 검증 필터
├── APILoginSuccessHandler.java  # 로그인 성공 처리
├── ApiUserDetailsService.java   # 사용자 상세 서비스
├── ApiUser.java                 # API 사용자 엔티티
├── ApiUserDTO.java              # API 사용자 DTO
├── ApiUserRepository.java       # API 사용자 저장소
└── AccessTokenException.java    # 토큰 예외 처리
```

### 2. Reply 패키지 (3개 파일)
```
reply/
├── ReplyController.java         # 게시글 REST API
├── ReplyEntity.java            # 게시글 엔티티
└── ReplyRepository.java        # 게시글 데이터 접근
```

### 3. Comment 패키지 (3개 파일)
```
comment/
├── CommentController.java       # 댓글 REST API
├── CommentEntity.java          # 댓글 엔티티
└── CommentRepository.java      # 댓글 데이터 접근
```

### 4. User 패키지 (1개 파일)
```
user/
└── UserEntity.java             # 사용자 엔티티
```

### 5. Util 패키지 (3개 파일)
```
util/
├── PageVO.java                 # 페이징 요청 객체
├── PageMaker.java              # 페이징 결과 객체
└── Download.java               # 파일 다운로드 컨트롤러
```

## 🛠️ 기술 스택 구조

```
Spring Boot Application
├── Spring Web (REST API)
├── Spring Security (JWT 인증)
├── Spring Data JPA (데이터 접근)
├── MySQL (데이터베이스)
├── Gradle (빌드 도구)
└── Lombok (코드 간소화)
```

## 📊 파일 통계

- **총 Java 파일**: 20개
- **메인 소스**: 17개
- **테스트 소스**: 3개
- **설정 파일**: 1개
- **데이터베이스 스키마**: 1개

## ✨ 주요 특징

### 1. 도메인 중심 패키징
- 기능별로 패키지가 명확히 분리됨
- 각 도메인(게시글, 댓글, 사용자, 보안)이 독립적으로 관리됨

### 2. 계층형 아키텍처
- **Controller**: REST API 엔드포인트 제공
- **Repository**: 데이터 접근 계층
- **Entity**: 데이터 모델 계층

### 3. 보안 중심 설계
- JWT 기반 인증 시스템
- Spring Security 필터 체인 구성
- API 사용자 관리 시스템

### 4. RESTful API
- 표준 REST API 설계 원칙 준수
- HTTP 메서드 적절한 활용
- 상태 코드 기반 응답

### 5. 페이징 지원
- 게시글 목록의 효율적인 페이징 처리
- 검색 기능과 연동된 페이징

### 6. 파일 업로드
- 첨부파일 기능 지원
- 파일 다운로드 기능

## 🔧 설정 파일 분석

### application.properties 주요 설정
```properties
# 기본 설정
spring.application.name=react_reply
server.port=8080

# 데이터베이스 설정
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
spring.datasource.url=jdbc:mysql://localhost:3306/react_reply
spring.datasource.username=testuser
spring.datasource.password=test1234

# 파일 업로드 설정
file.upload.path=D:\\upload
spring.servlet.multipart.enabled=true
spring.servlet.multipart.max-request-size=30MB
spring.servlet.multipart.max-file-size=10MB

# JPA 설정
spring.jpa.properties.hibernate.format_sql=true
spring.jpa.show-sql=true

# JWT 설정
jwt.secret.key=jwt_secret_key_123456789_!@#$%^&*(
```

## 📋 API 엔드포인트 목록

### 게시글 관련 API
- `GET /api/reply/list` - 게시글 목록 조회 (페이징, 검색)
- `POST /api/reply/regist` - 게시글 등록 (파일 업로드 포함)
- `GET /api/reply/view` - 게시글 상세 조회 (조회수 증가)
- `POST /api/reply/delete` - 게시글 삭제 (댓글도 함께 삭제)
- `GET /api/reply/edit` - 게시글 수정용 데이터 조회
- `POST /api/reply/update` - 게시글 수정 (파일 업로드/삭제)
- `POST /api/reply/reply` - 답변 등록

### 댓글 관련 API
- `GET /api/comment/list` - 특정 게시글의 댓글 목록
- `POST /api/comment/regist` - 댓글 등록
- `GET /api/comment/delete` - 개별 댓글 삭제
- `GET /api/comment/deleteAll` - 게시글의 모든 댓글 삭제

### 파일 관련 API
- `GET /download` - 파일 다운로드

### 인증 관련 API
- `POST /auth` - JWT 토큰 발급

## 🗄️ 데이터베이스 스키마

### 주요 테이블
1. **user** - 사용자 정보
2. **api_user** - API 인증용 사용자
3. **reply** - 게시글/답변 (계층형 구조)
4. **comment** - 댓글

### 계층형 게시글 구조
- **gno**: 그룹번호 (원글과 답변을 그룹화)
- **ono**: 순서 (같은 그룹 내 순서)
- **nested**: 깊이 (답변의 깊이)

## 🧪 테스트 구조

### 테스트 파일
- `ReactReplyApplicationTests.java` - 기본 애플리케이션 테스트
- `ReplyTest.java` - 게시글 기능 테스트
- `JwtTest.java` - JWT 토큰 테스트

## 📝 개발 환경

- **IDE**: IntelliJ IDEA / Eclipse
- **Java**: 17+
- **Spring Boot**: 3.x
- **Database**: MySQL 8.0
- **Build Tool**: Gradle
- **API Testing**: Postman

## 🚀 배포 환경

- **서버**: 로컬 개발 환경 (localhost:8080)
- **파일 저장**: D:\upload 디렉토리
- **데이터베이스**: MySQL 로컬 인스턴스

---

이 구조는 **Spring Boot 기반의 표준적인 웹 애플리케이션** 구조를 따르고 있으며, 각 계층이 명확히 분리되어 유지보수성이 좋은 설계입니다. 