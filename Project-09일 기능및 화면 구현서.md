#### 회원관리 및 유저
- 회원가입/로그인/로그아웃 화면 
- 내 정보/회원 정보 수정 화면 
-  팔로잉/팔로워 목록 화면  
#### 상품관리
  - 상품 목록/상세/등록/수정/삭제 화면 
  - 상품 이미지 및 파일 업로드/다운로드 
  - 즐겨찾기(찜) 목록 
  - 댓글/후기 목록 및 작성 화면  
#### 거래/구매/판매
- 거래 내역/판매 후기/구독 상품 목록 및 상세 화면 
-  후기 작성/수정/삭제 화면 
#### QNA
- Q&A 목록/상세/작성/수정/삭제 화면 
- 답변 등록/수정/삭제 화면  
#### 채팅/메시지
 - 채팅방 목록/입장/채팅 화면
- 메시지 전송/수신 화면
#### 공지사항/게시판 (board)
 - 공지사항 목록/상세/작성/수정/삭제 화면
#### 역 목록/상세/등록/수정/삭제 화면  
- 역 목록/상세/등록/수정/삭제 화면  
	- 역 삭제가 필요할까?? 역에 핑 찍는 정도만 되면 될듯 싶달까요
####  광고
-  광고 목록/상세/등록/수정/삭제 화면  
#### 카테고리 (CATEGORY)
 - 카테고리 목록/등록/수정/삭제 화면  
#### 관리자 (ADMIN)
- 관리자 로그인/로그아웃 
- 전체 데이터 관리(회원, 상품, 거래, 광고, 공지 등) 
#### 담구기 기능 
- 우리 프젝의 핵심 및 토이 기능 
### 필수 구현기능 -  핵심구현  
1. 회원관리 및 유저
2. 상품관리
3. 거래/구매/판매
4. 채팅/메시지
5. 공지사항/게시판 (board)
6. 카테고리 (CATEGORY)
7. 관리자 (ADMIN)
8. 담구기 기능`
### 부가 구현기능 - 추가구현
1. 광고
2. 역 목록/상세/등록/수정/삭제 화면  ==보류== 
3. QNA




---


1. 회원 관리 (USER_INFO, USER_FILE, FOLLOW)
Model
회원 정보: USER_INFO
회원 파일(프로필 등): USER_FILE
팔로우 관계: FOLLOW
View
회원가입/로그인/로그아웃 화면
내 정보/회원 정보 수정 화면
팔로잉/팔로워 목록 화면
Controller
회원 가입/로그인/로그아웃 요청 처리
회원 정보 조회/수정/삭제
프로필 이미지 업로드/다운로드
팔로우/언팔로우 기능 처리

2. 상품 관리 (PRODUCT, PD_FILE, FAVORITE, COMMENT_FIELD)
Model
상품 정보: PRODUCT
상품 파일(이미지 등): PD_FILE
즐겨찾기(찜): FAVORITE
상품 댓글/후기: COMMENT_FIELD
View
상품 목록/상세/등록/수정/삭제 화면
상품 이미지 및 파일 업로드/다운로드
즐겨찾기(찜) 목록
댓글/후기 목록 및 작성 화면
Controller
상품 등록/수정/삭제/조회
상품 이미지 및 파일 관리
즐겨찾기(찜) 추가/삭제
댓글/후기 작성/수정/삭제/조회

3. 거래/구매/판매 이력 (TRADE_HISTORY, SALE_REVIEW, subscription)
Model
거래 이력: TRADE_HISTORY
판매 후기: SALE_REVIEW
구독 정보: subscription
View
거래 내역/판매 후기/구독 상품 목록 및 상세 화면
후기 작성/수정/삭제 화면
Controller
거래 이력 등록/조회
판매 후기 작성/수정/삭제
구독 상품 등록/해지/조회

4. Q&A 및 문의 (USERQNA_INFO, ANSWER_INFO)
Model
문의(Q&A): USERQNA_INFO
답변: ANSWER_INFO
View
Q&A 목록/상세/작성/수정/삭제 화면
답변 등록/수정/삭제 화면
Controller
Q&A 등록/수정/삭제/조회
답변 등록/수정/삭제/조회

5. 채팅/메시지 (CHAT_ROOM, MESSAGE)
Model
채팅방: CHAT_ROOM
메시지: MESSAGE
View
채팅방 목록/입장/채팅 화면
메시지 전송/수신 화면
Controller
채팅방 생성/입장/퇴장
메시지 전송/수신/조회

6. 공지사항/게시판 (board)
Model
공지사항: board
View
공지사항 목록/상세/작성/수정/삭제 화면
Controller
공지사항 등록/수정/삭제/조회


7. 역 정보 (STATION)
Model
역 정보: STATION
View
역 목록/상세/등록/수정/삭제 화면
Controller
역 정보 등록/수정/삭제/조회


8. 광고 (ADVERTISEMENT)
Model
광고: ADVERTISEMENT
View
광고 목록/상세/등록/수정/삭제 화면
Controller
광고 등록/수정/삭제/조회


9. 카테고리 (CATEGORY)
Model
카테고리: CATEGORY
View
카테고리 목록/등록/수정/삭제 화면
Controller
카테고리 등록/수정/삭제/조회


10. 관리자 (ADMIN)
Model
관리자: ADMIN
View
관리자 로그인/관리 화면
Controller
관리자 로그인/로그아웃
전체 데이터 관리(회원, 상품, 거래, 광고, 공지 등)

요약 표
도메인ModelViewController회원USER_INFO, USER_FILE, FOLLOW회원가입/정보/팔로우 화면회원/팔로우/파일 관리상품PRODUCT, PD_FILE, FAVORITE, COMMENT_FIELD상품/찜/댓글 화면상품/찜/댓글 관리거래/후기/구독TRADE_HISTORY, SALE_REVIEW, subscription거래/후기/구독 화면거래/후기/구독 관리Q&AUSERQNA_INFO, ANSWER_INFOQ&A/답변 화면Q&A/답변 관리채팅/메시지CHAT_ROOM, MESSAGE채팅/메시지 화면채팅/메시지 관리공지사항board공지사항 화면공지사항 관리역 정보STATION역 정보 화면역 정보 관리광고ADVERTISEMENT광고 화면광고 관리카테고리CATEGORY카테고리 화면카테고리 관리관리자ADMIN관리자 화면관리자 기능 관리


