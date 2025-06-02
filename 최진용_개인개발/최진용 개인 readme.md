## 🔧 Key Technologies / 주요 기술 스택

- **Spring Framework 5.3.39**
- **MyBatis 3.5.16**
- **Oracle Database**
- **Lombok**
- **WebSocket (for 실시간 채팅)**
- **Spring Security (로그인 인증용)**
- **Gson / Jackson (JSON 직렬화)**


## 🧱 Database Tables / 데이터베이스 테이블

### 1. `CHAT_ROOM` (채팅방)
| 컬럼명      | 타입              | 설명                  |
|------------|-------------------|-----------------------|
| ROOM_NO    | NUMBER(11)        | 채팅방 번호 (PK)      |
| USER_ID    | VARCHAR2(255)     | 유저 ID (복합 PK)     |
| LASTVISIT  | VARCHAR2(20)      | 마지막 방문 시간 정보 |
| CHAT_TYPE  | VARCHAR2(20)      | 일반/이미지 채팅 구분 |

### 2. `MESSAGE` (메시지)
| 컬럼명      | 타입              | 설명                  |
|------------|-------------------|-----------------------|
| NO         | NUMBER(11)        | 메시지 번호 (PK)      |
| ROOM_NO    | NUMBER(11)        | 채팅방 번호 (FK)      |
| MESSAGE    | CLOB              | 텍스트 메시지 내용     |
| IMAGE_URL  | VARCHAR2(255)     | 이미지 URL (선택)     |
| USER_ID    | VARCHAR2(255)     | 보낸 사람 ID          |
| SEND_TIME  | DATE              | 보낸 시간             |

---

## 💡 Implementation Plan / 구현 계획

### 🔸 1. Controller Layer
- **`ChatController`**  
  - 채팅방 생성, 입장, 메시지 목록 요청 처리  
  - WebSocket 연결 엔드포인트 제공 예정

### 🔸 2. Service Layer
- **`ChatService` / `ChatServiceImpl`**  
  - 채팅방 로직 처리 (생성, 유저 매핑, 시간 업데이트)  
  - 메시지 등록/조회 처리

### 🔸 3. DAO Layer
- **`ChatDAO` (class형 DAO)**  
  - MyBatis 사용하여 DB 연결  
  - `chat-mapper.xml`과 연동하여 채팅방/메시지 CRUD 처리

### 🔸 4. View Layer
- **JSP 사용**
  - 채팅방 목록 / 채팅 화면 구현
  - AJAX 사용 또는 WebSocket JS 클라이언트로 실시간 메시지 처리

---

## ✅ 기능 명세 / 구현할 기능 목록

### ⭐ 핵심 기능
- [ ] 채팅방 생성 및 입장/퇴장
- [ ] 실시간 메시지 송수신 (WebSocket)
- [ ] 댓글(메시지) 등록 및 조회

### 🔽 세부 기능
- [ ] 이미지 포함 채팅
- [ ] 채팅방 목록/삭제
- [ ] 메시지 수정/삭제
- [ ] 팔로우/언팔로우 기능
- [ ] 알림 기능 (예: 팔로우/댓글 알림)

---

## 📌 Best Practices / 개발 시 지켜야 할 원칙

- MVC 구조 철저 분리
- DAO는 인터페이스 없이 클래스 기반으로 구성
- 비즈니스 로직은 반드시 Service에서 처리
- 모든 SQL은 `mapper.xml`에 정리
- VO에는 Lombok 사용 (@Getter, @Setter, @ToString 등)
- 메시지 송수신 시간은 `SimpleDateFormat` 또는 DB의 `SYSDATE` 활용

---

## ⏭️ 다음 단계 추천

1. JSP에서 채팅방 목록 및 입장 페이지 구성
2. WebSocket 환경 설정 및 Echo 테스트
3. JavaScript로 WebSocket 연결 구현
4. 이미지 메시지 전송 구현 (MultipartFile → 저장 후 URL 저장)
5. 사용자 알림 및 읽음 처리 구현

---

필요하면 이 마크다운은 README.md로 저장해서 프로젝트 루트에 추가하면 돼.  
다음으로 **JSP 화면 구성할지**, **WebSocket 연결할지** 선택만 해 줘! 😎