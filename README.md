# 🌐 React 기반 스마트팜 IoT 기기 연동 및 식물 성장 대시보드・모니터링 구축

[![Notion](https://img.shields.io/badge/Notion-Details-F7F6F3?style=flat&logo=notion&logoColor=000000)](https://is.gd/QzNXbB)
[![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.4.1-6DB33F?style=flat&logo=springboot&logoColor=white)](https://spring.io/projects/spring-boot)
[![React](https://img.shields.io/badge/React-19-61DAFB?style=flat&logo=react&logoColor=black)](https://react.dev/)
[![Java](https://img.shields.io/badge/Java-17-007396?style=flat&logo=openjdk&logoColor=white)](https://www.oracle.com/java/)
[![MariaDB](https://img.shields.io/badge/MariaDB-10.x-003545?style=flat&logo=mariadb&logoColor=white)](https://mariadb.org/)

## 📋 목차

- [프로젝트 개요](#-프로젝트-개요)
- [주요 기능](#-주요-기능)
- [기술 스택](#-기술-스택)
- [시스템 구조](#-시스템-구조)
- [시작하기](#-시작하기)
- [주요 성과](#-주요-성과)
- [트러블슈팅](#-트러블슈팅)
- [프로젝트 통계](#-프로젝트-통계)
- [라이선스](#-라이선스)

## 📌 프로젝트 개요

**개발 기간** : 2025.09.12 ~ 2025.10.13 (32일)

**프로젝트 목표** : 농작물 생육 환경을 실시간으로 모니터링하기 위한 IoT 기반 웹 시스템 구축

**핵심 성과** :
- 기존 11명 사용자 비밀번호를 BCrypt로 암호화해 보안 수준 강화
- 실시간 유효성 검사 및 중복 코드 87.5% 제거 (8곳 → 1개 함수)
- Gmail SMTP 기반 이메일 인증 및 임시 비밀번호 발급 시스템 구현
- 20개 이상의 실질적 문제 해결 경험

## ✨ 주요 기능

### 1️⃣ 회원가입 시스템
정규표현식 기반 실시간 유효성 검사, 아이디 중복 확인 API, 이메일 인증, 필수 약관 동의, `BCrypt` 단방향 암호화를 구현했습니다.

**주요 성과**
- `validation.jsx`로 유효성 검사 로직 통합 (중복 코드 8곳 → 1곳, 87.5% 개선)
- 실시간 유효성 검사로 즉각적인 피드백 제공
- 아이디 중복 확인으로 가입 실패 사전 방지

### 2️⃣ 로그인 시스템
`POST` 방식 인증, `BCrypt` 비밀번호 검증, 아이디 저장 `localStorage`, 세션 관리 `sessionStorage`, 탭 기반 아이디·비밀번호 찾기를 구현했습니다.

**주요 성과**
- `POST` 방식으로 URL 내 비밀번호 노출 방지
- HTTP 상태 코드 기반 명확한 에러 메시지 반환
- `sessionStorage`로 탭 종료 시 자동 로그아웃 처리

### 3️⃣ 이메일 인증 시스템
Gmail SMTP 연동, 6자리 인증번호 생성, 5분 타이머, HTML 베이지 톤 템플릿 디자인, 임시 비밀번호 발급 기능을 구현했습니다.

**주요 성과**
- Gmail SMTP 연동으로 자체 발송 시스템 구축
- 앱 비밀번호를 통한 Gmail 2단계 인증 준수
- `useEffect` `cleanup`으로 타이머 메모리 누수 방지
- 베이지 톤 HTML 템플릿으로 브랜드 통일

### 4️⃣ 보안 시스템
평문 비밀번호를 `BCrypt`로 암호화하는 마이그레이션, `Salt` 자동 생성, 단방향 암호화로 복호화 불가, 데이터베이스 `VARCHAR(100)` 확장을 구현했습니다.

**주요 성과**
- 기존 11명 사용자 비밀번호를 `BCrypt`로 안전하게 암호화
- `Salt` 자동 생성으로 Rainbow Table 공격 방어
- 아이디 마스킹으로 개인정보 보호 강화

## 🔧 기술 스택

### 백엔드
- **언어**: Java 17
- **프레임워크**: Spring Boot 3.4.1
- **데이터베이스**: MariaDB
- **보안**: BCrypt 암호화
- **이메일**: Gmail SMTP

### 프론트엔드
- **언어**: JavaScript
- **프레임워크**: React 19
- **빌드 도구**: Vite
- **스타일링**: CSS Modules

## 🏗️ 시스템 구조

### 전체 아키텍처
```
📦 backend_root (Spring Boot)
├── 📁 answer
├── 📁 application
├── 📁 common
├── 📁 config
├── 📁 counter
├── 📁 email                    # 이메일 인증 시스템
│   ├── controller/EmailController
│   ├── dto/EmailSendDTO, EmailVerifyDTO
│   └── service/EmailService
├── 📁 growing
├── 📁 motionBuzzer
├── 📁 notice
├── 📁 plantBot
├── 📁 question
├── 📁 schedule
└── 📁 user                      # 회원 관리 시스템
    ├── controller/UserController
    ├── dto/UserDTO
    ├── mapper/UserMapper
    └── service/UserService
```
```
📦 frontend_root (React)
└── src
    ├── 📁 assets
    ├── 📁 common
    │   ├── Accordion.jsx           # 약관 아코디언 컴포넌트
    │   └── Modal.jsx               # 공통 모달 컴포넌트
    ├── 📁 component
    ├── 📁 constants
    ├── 📁 hooks
    │   └── useAgreements.js        # 약관 동의 커스텀 훅
    ├── 📁 layout
    ├── 📁 pages
    │   ├── 📁 admin
    │   ├── 📁 main
    │   ├── 📁 menu
    │   └── 📁 user              　　# 회원 관리 페이지
    │       ├── EmailAuth.jsx       # 이메일 인증
    │       ├── Join.jsx            # 회원가입
    │       └── Login.jsx           # 로그인
    └── 📁 utils
        └── validation.jsx          # 유효성 검사 함수
```

### 데이터베이스 구조
```sql
CREATE TABLE USERS (
    USER_ID VARCHAR(20) PRIMARY KEY,
    USER_PW VARCHAR(100) NOT NULL,
    USER_NAME VARCHAR(20) NOT NULL,
    USER_TEL VARCHAR(15),
    USER_EMAIL VARCHAR(50) UNIQUE,
    USER_ROLE VARCHAR(10) DEFAULT 'USER',
    CREATE_DATE DATETIME DEFAULT SYSDATE()
);
```

## 🚀 시작하기

### 시스템 요구사항
- Java 17 이상
- Node.js 18 이상
- MariaDB 10.x
- Spring Boot 3.4.1
- React 19

### 설치 방법

#### 백엔드 설정
```bash
# Spring Boot 의존성 설치 (Maven/Gradle 사용)
./mvnw install

# 또는 Gradle 사용 시
./gradlew build
```

#### 프론트엔드 설정
```bash
# npm 패키지 설치
npm install

# 또는 yarn 사용 시
yarn install
```

#### 데이터베이스 설정
```sql
-- 데이터베이스 생성
CREATE DATABASE ...;

-- 회원 테이블 생성
CREATE TABLE USERS (
    USER_ID VARCHAR(20) PRIMARY KEY,
    USER_PW VARCHAR(100) NOT NULL,
    USER_NAME VARCHAR(20) NOT NULL,
    USER_TEL VARCHAR(15),
    USER_EMAIL VARCHAR(50) UNIQUE,
    USER_ROLE VARCHAR(10) DEFAULT 'USER',
    CREATE_DATE DATETIME DEFAULT SYSDATE()
);
```

#### 환경 변수 설정
`application.properties` 또는 `application.yml`에서 데이터베이스 및 이메일 설정:
```properties
# 데이터베이스 설정
spring.datasource.url=jdbc:mariadb://...
spring.datasource.username=...
spring.datasource.password=...

# Gmail SMTP 설정
spring.mail.host=smtp.gmail.com
spring.mail.port=587
spring.mail.username=...
spring.mail.password=...
```

### 실행 방법

#### 백엔드 실행
```bash
# Spring Boot 애플리케이션 실행
./mvnw spring-boot:run

# 또는 Gradle 사용 시
./gradlew bootRun
```

#### 프론트엔드 실행
```bash
# 개발 서버 실행
npm run dev

# 또는 yarn 사용 시
yarn dev
```

## 🏆 주요 성과

### 시스템 보안 및 개인정보 보호 강화
- 기존 11명 회원 비밀번호를 `BCrypt`로 안전하게 마이그레이션
- `Salt` 자동 생성으로 Rainbow Table 공격 방어
- `POST` 방식 적용으로 URL 내 비밀번호 노출 위험 제거
- `sessionStorage` 기반으로 탭 종료 시 자동 로그아웃 처리
- 아이디 찾기 결과 마스킹 처리로 개인정보 보호 강화

### 코드 효율성 및 재사용성 향상
- `validation.jsx`로 중복 코드 8곳 → 1곳 통합 (87.5% 개선)
- `useAgreements` 커스텀 훅으로 약관 로직 분리 및 재사용성 확보
- 입력 검증, 회원가입, 로그인, 비밀번호 복구 전 과정에 `BCrypt` 암호화 일관 적용

### 시스템 안정성 및 이메일 통신 구조 확립
- Gmail SMTP 연동으로 자체 이메일 발송 시스템 구축
- `useEffect` cleanup 함수로 타이머 메모리 누수 방지
- Git 단계별 커밋으로 안전한 마이그레이션 절차 확립
- 베이지 톤 HTML 템플릿으로 브랜드 시각 일관성 확보

## 🐛 트러블슈팅

### BCrypt 비밀번호 마이그레이션
**증상** : 기존 평문 비밀번호를 암호화로 전환할 필요 발생

**원인** : 데이터베이스 보안 취약점 및 `VARCHAR(20)` 길이 부족

**조치** : `VARCHAR(100)`으로 확장 후 일회성 마이그레이션 메서드로 11명 사용자 비밀번호 일괄 변환

**결과** : 데이터베이스 보안 강화 및 데이터 무결성 유지

**교훈** : Git 단계별 커밋으로 안전한 마이그레이션 절차 확립 필요

### React State 비동기 처리
**증상** : `setState` 직후 값 읽기 시 이전 값 반환

**원인** : React의 비동기 State 업데이트 특성

**조치** : 함수형 업데이트 `prev => prev + 1` 및 파라미터로 최신 값 전달

**결과** : State 관리 안정성 확보

**교훈** : React의 비동기 State 업데이트 메커니즘 이해 필요

### 타이머 메모리 누수
**증상** : 인증번호 재발송 시 타이머가 2개 이상 동시 실행

**원인** : `useEffect` cleanup 함수 누락

**조치** : `return () => clearInterval(countdown)` 추가

**결과** : 메모리 누수 방지 및 타이머 정상 동작

**교훈** : React `cleanup` 함수를 통한 리소스 정리 필수

## 📊 프로젝트 통계

| 항목 | 수치 |
|------|------|
| 개발 기간 | 32일 |
| 코드 라인 | 약 2,000줄 |
| 백엔드 파일 | 9개 |
| 프론트엔드 파일 | 10개 |
| 테이블 | 8개 |
| 해결한 문제 | 20개 이상 |

## 📄 라이선스

이 프로젝트는 포트폴리오 목적으로 제작되었습니다.

**© 2025 root**