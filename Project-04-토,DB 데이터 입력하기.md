## DB 테이블 및 기본 데이터 - 장유진, 양찬우
 
#### 사용자계정 생성
```sql
CREATE USER DAMGEUN IDENTIFIED BY DAMGEUN;
--권한 부여하기
GRANT RESOURCE, CONNECT TO DAMGEUN;
```

#### 유저 테이블 생성
```SQL
  CREATE TABLE "DAMGEUN"."USER_INFO" 
   (	"USERNO" NUMBER(11,0) NOT NULL ENABLE, 
	"USERID" VARCHAR2(255) NOT NULL ENABLE, 
	"PASSWORD" VARCHAR2(255) NOT NULL ENABLE, 
	"USERNAME" VARCHAR2(20) NOT NULL ENABLE, 
	"EMAIL" VARCHAR2(255), 
	"STATUS" VARCHAR2(1) DEFAULT 'Y' NOT NULL ENABLE, 
	"USERRANK" NUMBER(*,0) DEFAULT 100, 
	 CONSTRAINT "USER_INFO_PK" PRIMARY KEY ("USERNO")
  USING INDEX PCTFREE 10 INITRANS 2 MAXTRANS 255 COMPUTE STATISTICS 
  STORAGE(INITIAL 65536 NEXT 1048576 MINEXTENTS 1 MAXEXTENTS 2147483645
  PCTINCREASE 0 FREELISTS 1 FREELIST GROUPS 1 BUFFER_POOL DEFAULT FLASH_CACHE DEFAULT CELL_FLASH_CACHE DEFAULT)
  TABLESPACE "SYSTEM"  ENABLE
   ) SEGMENT CREATION IMMEDIATE 
  PCTFREE 10 PCTUSED 40 INITRANS 1 MAXTRANS 255 NOCOMPRESS LOGGING
  STORAGE(INITIAL 65536 NEXT 1048576 MINEXTENTS 1 MAXEXTENTS 2147483645
  PCTINCREASE 0 FREELISTS 1 FREELIST GROUPS 1 BUFFER_POOL DEFAULT FLASH_CACHE DEFAULT CELL_FLASH_CACHE DEFAULT)
  TABLESPACE "SYSTEM";

   COMMENT ON COLUMN "DAMGEUN"."USER_INFO"."USERNO" IS '유저번호 (유저 이미지나 영상 판매물품 외례키)';
   COMMENT ON COLUMN "DAMGEUN"."USER_INFO"."USERID" IS '유저아이디';
   COMMENT ON COLUMN "DAMGEUN"."USER_INFO"."PASSWORD" IS '유저비밀번호';
   COMMENT ON COLUMN "DAMGEUN"."USER_INFO"."USERNAME" IS '유저이름(닉네임)';
   COMMENT ON COLUMN "DAMGEUN"."USER_INFO"."EMAIL" IS '이메일';
   COMMENT ON COLUMN "DAMGEUN"."USER_INFO"."STATUS" IS '유저상태(회원 탈퇴 유무)';
   COMMENT ON COLUMN "DAMGEUN"."USER_INFO"."USERRANK" IS '유저 매너 지수';
```

#### 유저 파일 테이블 생성
```SQL
 CREATE TABLE "DAMGEUN"."USER_FILE" 
   (	"USERNO" NUMBER(11,0) NOT NULL ENABLE, 
	"FILEURL" VARCHAR2(255), 
	"FILETYPE" VARCHAR2(20) DEFAULT 'IMG', 
	 CONSTRAINT "USER_FILE_PK" PRIMARY KEY ("USERNO")
  USING INDEX PCTFREE 10 INITRANS 2 MAXTRANS 255 
  STORAGE(INITIAL 65536 NEXT 1048576 MINEXTENTS 1 MAXEXTENTS 2147483645
  PCTINCREASE 0 FREELISTS 1 FREELIST GROUPS 1 BUFFER_POOL DEFAULT FLASH_CACHE DEFAULT CELL_FLASH_CACHE DEFAULT)
  TABLESPACE "SYSTEM"  ENABLE, 
	 CONSTRAINT "USERNUM" FOREIGN KEY ("USERNO")
	  REFERENCES "DAMGEUN"."USER_INFO" ("USERNO") ENABLE
   ) SEGMENT CREATION IMMEDIATE 
  PCTFREE 10 PCTUSED 40 INITRANS 1 MAXTRANS 255 NOCOMPRESS LOGGING
  STORAGE(INITIAL 65536 NEXT 1048576 MINEXTENTS 1 MAXEXTENTS 2147483645
  PCTINCREASE 0 FREELISTS 1 FREELIST GROUPS 1 BUFFER_POOL DEFAULT FLASH_CACHE DEFAULT CELL_FLASH_CACHE DEFAULT)
  TABLESPACE "SYSTEM"; 

   COMMENT ON COLUMN "DAMGEUN"."USER_FILE"."USERNO" IS '유저 번호 USERINFO참조';
   COMMENT ON COLUMN "DAMGEUN"."USER_FILE"."FILEURL" IS '파일URL';
   COMMENT ON COLUMN "DAMGEUN"."USER_FILE"."FILETYPE" IS '이미지인지 또는 프로필사진인지';
```


#### 상품 게시글 테이블 생성
```Sql
  CREATE TABLE "DAMGEUN"."PRODUCT" 
   (	"USERNO" NUMBER(11,0) NOT NULL ENABLE, 
	"PD_NUM" NUMBER(11,0) NOT NULL ENABLE, 
	"PD_TITLE" VARCHAR2(255) NOT NULL ENABLE, 
	"PD_BOARD" CLOB NOT NULL ENABLE, 
	"PD_PRICE" VARCHAR2(20) NOT NULL ENABLE, 
	"LATITUDE" VARCHAR2(20) NOT NULL ENABLE, 
	"LONGITUDE" VARCHAR2(20) NOT NULL ENABLE, 
	"BIG_CATA" VARCHAR2(20), 
	"MID_CATA" VARCHAR2(20), 
	"SMALL_CATA" VARCHAR2(20), 
	"UPDATE_TIME" DATE NOT NULL ENABLE, 
	"PD_RANK" NUMBER(4,0) DEFAULT 1000 NOT NULL ENABLE, 
	 CONSTRAINT "PRODUCT_PK" PRIMARY KEY ("USERNO", "PD_NUM")
  USING INDEX PCTFREE 10 INITRANS 2 MAXTRANS 255 COMPUTE STATISTICS 
  STORAGE(INITIAL 65536 NEXT 1048576 MINEXTENTS 1 MAXEXTENTS 2147483645
  PCTINCREASE 0 FREELISTS 1 FREELIST GROUPS 1 BUFFER_POOL DEFAULT FLASH_CACHE DEFAULT CELL_FLASH_CACHE DEFAULT)
  TABLESPACE "SYSTEM"  ENABLE, 
	 CONSTRAINT "USER_PD_NUM" FOREIGN KEY ("USERNO")
	  REFERENCES "DAMGEUN"."USER_INFO" ("USERNO") ENABLE
   ) SEGMENT CREATION IMMEDIATE 
  PCTFREE 10 PCTUSED 40 INITRANS 1 MAXTRANS 255 NOCOMPRESS LOGGING
  STORAGE(INITIAL 65536 NEXT 1048576 MINEXTENTS 1 MAXEXTENTS 2147483645
  PCTINCREASE 0 FREELISTS 1 FREELIST GROUPS 1 BUFFER_POOL DEFAULT FLASH_CACHE DEFAULT CELL_FLASH_CACHE DEFAULT)
  TABLESPACE "SYSTEM" 
 LOB ("PD_BOARD") STORE AS BASICFILE (
  TABLESPACE "SYSTEM" ENABLE STORAGE IN ROW CHUNK 8192 RETENTION 
  NOCACHE LOGGING 
  STORAGE(INITIAL 65536 NEXT 1048576 MINEXTENTS 1 MAXEXTENTS 2147483645
  PCTINCREASE 0 FREELISTS 1 FREELIST GROUPS 1 BUFFER_POOL DEFAULT FLASH_CACHE DEFAULT CELL_FLASH_CACHE DEFAULT));

   COMMENT ON COLUMN "DAMGEUN"."PRODUCT"."USERNO" IS '유저 번호';
   COMMENT ON COLUMN "DAMGEUN"."PRODUCT"."PD_NUM" IS '상품번호';
   COMMENT ON COLUMN "DAMGEUN"."PRODUCT"."PD_TITLE" IS '상품제목';
   COMMENT ON COLUMN "DAMGEUN"."PRODUCT"."PD_BOARD" IS '상품내용';
   COMMENT ON COLUMN "DAMGEUN"."PRODUCT"."PD_PRICE" IS '상품가격';
   COMMENT ON COLUMN "DAMGEUN"."PRODUCT"."LATITUDE" IS '위도';
   COMMENT ON COLUMN "DAMGEUN"."PRODUCT"."LONGITUDE" IS '경도';
   COMMENT ON COLUMN "DAMGEUN"."PRODUCT"."BIG_CATA" IS '대분류(카테고리)';
   COMMENT ON COLUMN "DAMGEUN"."PRODUCT"."MID_CATA" IS '중분류(카테고리)';
   COMMENT ON COLUMN "DAMGEUN"."PRODUCT"."SMALL_CATA" IS '소분류(카테고리)';
   COMMENT ON COLUMN "DAMGEUN"."PRODUCT"."UPDATE_TIME" IS '업로드시간';
   COMMENT ON COLUMN "DAMGEUN"."PRODUCT"."PD_RANK" IS '상품점수(담그기용)';
```

#### 상품별 첨부 파일 (이미지 동영상)테이블
```SQL
  CREATE TABLE "DAMGEUN"."PD_FILE" 
   (	"USERNO" NUMBER(11,0) NOT NULL ENABLE, 
	"PD_NUM" NUMBER(11,0) NOT NULL ENABLE, 
	"PD_URL" VARCHAR2(255) NOT NULL ENABLE, 
	"FILETYPE" VARCHAR2(20) DEFAULT 'IMG' NOT NULL ENABLE, 
	"ISTHUMBNAIL" VARCHAR2(20) DEFAULT 'N' NOT NULL ENABLE, 
	 CONSTRAINT "PD_FILE_PK" PRIMARY KEY ("PD_NUM", "USERNO")
  USING INDEX PCTFREE 10 INITRANS 2 MAXTRANS 255 COMPUTE STATISTICS 
  STORAGE(INITIAL 65536 NEXT 1048576 MINEXTENTS 1 MAXEXTENTS 2147483645
  PCTINCREASE 0 FREELISTS 1 FREELIST GROUPS 1 BUFFER_POOL DEFAULT FLASH_CACHE DEFAULT CELL_FLASH_CACHE DEFAULT)
  TABLESPACE "SYSTEM"  ENABLE, 
	 CONSTRAINT "PD_FILE_FK1" FOREIGN KEY ("USERNO", "PD_NUM")
	  REFERENCES "DAMGEUN"."PRODUCT" ("USERNO", "PD_NUM") ON DELETE CASCADE ENABLE
   ) SEGMENT CREATION IMMEDIATE 
  PCTFREE 10 PCTUSED 40 INITRANS 1 MAXTRANS 255 NOCOMPRESS LOGGING
  STORAGE(INITIAL 65536 NEXT 1048576 MINEXTENTS 1 MAXEXTENTS 2147483645
  PCTINCREASE 0 FREELISTS 1 FREELIST GROUPS 1 BUFFER_POOL DEFAULT FLASH_CACHE DEFAULT CELL_FLASH_CACHE DEFAULT)
  TABLESPACE "SYSTEM"; 

   COMMENT ON COLUMN "DAMGEUN"."PD_FILE"."USERNO" IS '유저번호';
   COMMENT ON COLUMN "DAMGEUN"."PD_FILE"."PD_NUM" IS '상품번호';
   COMMENT ON COLUMN "DAMGEUN"."PD_FILE"."PD_URL" IS '파일URL';
   COMMENT ON COLUMN "DAMGEUN"."PD_FILE"."FILETYPE" IS '파일타입';
   COMMENT ON COLUMN "DAMGEUN"."PD_FILE"."ISTHUMBNAIL" IS '썸네일여부';
```

#### 채팅방 테이블 생성
```SQL
  CREATE TABLE "DAMGEUN"."CHAT_ROOM" 
   (	"ROOMNO" NUMBER(11,0) NOT NULL ENABLE, 
	"USERID" VARCHAR2(255) NOT NULL ENABLE, 
	"LASTVISIT" VARCHAR2(20) NOT NULL ENABLE, 
	"CHATTYPE" VARCHAR2(20) NOT NULL ENABLE, 
	 CONSTRAINT "CHAT_ROOM_PK" PRIMARY KEY ("ROOMNO")
  USING INDEX PCTFREE 10 INITRANS 2 MAXTRANS 255 
  STORAGE(INITIAL 65536 NEXT 1048576 MINEXTENTS 1 MAXEXTENTS 2147483645
  PCTINCREASE 0 FREELISTS 1 FREELIST GROUPS 1 BUFFER_POOL DEFAULT FLASH_CACHE DEFAULT CELL_FLASH_CACHE DEFAULT)
  TABLESPACE "SYSTEM"  ENABLE
   ) SEGMENT CREATION IMMEDIATE 
  PCTFREE 10 PCTUSED 40 INITRANS 1 MAXTRANS 255 NOCOMPRESS LOGGING
  STORAGE(INITIAL 65536 NEXT 1048576 MINEXTENTS 1 MAXEXTENTS 2147483645
  PCTINCREASE 0 FREELISTS 1 FREELIST GROUPS 1 BUFFER_POOL DEFAULT FLASH_CACHE DEFAULT CELL_FLASH_CACHE DEFAULT)
  TABLESPACE "SYSTEM";

   COMMENT ON COLUMN "DAMGEUN"."CHAT_ROOM"."ROOMNO" IS '채팅방번호';
   COMMENT ON COLUMN "DAMGEUN"."CHAT_ROOM"."USERID" IS '유저 ID(ABC123@TEST123)';
   COMMENT ON COLUMN "DAMGEUN"."CHAT_ROOM"."LASTVISIT" IS '마지막방문 EX)ABC123(날짜시간)@TEST123(날짜시간)';
   COMMENT ON COLUMN "DAMGEUN"."CHAT_ROOM"."CHATTYPE" IS '채팅타입(이미지 채팅인지 일반 채팅인지)';
```

#### 메시지 테이블 생성
```sql
  CREATE TABLE "DAMGEUN"."MESSAGE" 
   (	"ROOMNO" NUMBER(11,0) NOT NULL ENABLE, 
	"NO" NUMBER(11,0) NOT NULL ENABLE, 
	"MESSAGE" CLOB NOT NULL ENABLE, 
	"IMAGEURL" VARCHAR2(255) NOT NULL ENABLE, 
	"USERID" VARCHAR2(255) NOT NULL ENABLE, 
	"SENDTIME" DATE NOT NULL ENABLE, 
	 CONSTRAINT "MESSAGE_PK" PRIMARY KEY ("NO", "ROOMNO")
  USING INDEX PCTFREE 10 INITRANS 2 MAXTRANS 255 
  STORAGE(INITIAL 65536 NEXT 1048576 MINEXTENTS 1 MAXEXTENTS 2147483645
  PCTINCREASE 0 FREELISTS 1 FREELIST GROUPS 1 BUFFER_POOL DEFAULT FLASH_CACHE DEFAULT CELL_FLASH_CACHE DEFAULT)
  TABLESPACE "SYSTEM"  ENABLE, 
	 CONSTRAINT "ROOM_NO_FK" FOREIGN KEY ("ROOMNO")
	  REFERENCES "DAMGEUN"."CHAT_ROOM" ("ROOMNO") ENABLE
   ) SEGMENT CREATION IMMEDIATE 
  PCTFREE 10 PCTUSED 40 INITRANS 1 MAXTRANS 255 NOCOMPRESS LOGGING
  STORAGE(INITIAL 65536 NEXT 1048576 MINEXTENTS 1 MAXEXTENTS 2147483645
  PCTINCREASE 0 FREELISTS 1 FREELIST GROUPS 1 BUFFER_POOL DEFAULT FLASH_CACHE DEFAULT CELL_FLASH_CACHE DEFAULT)
  TABLESPACE "SYSTEM" 
 LOB ("MESSAGE") STORE AS BASICFILE (
  TABLESPACE "SYSTEM" ENABLE STORAGE IN ROW CHUNK 8192 RETENTION 
  NOCACHE LOGGING 
  STORAGE(INITIAL 65536 NEXT 1048576 MINEXTENTS 1 MAXEXTENTS 2147483645
  PCTINCREASE 0 FREELISTS 1 FREELIST GROUPS 1 BUFFER_POOL DEFAULT FLASH_CACHE DEFAULT CELL_FLASH_CACHE DEFAULT));

   COMMENT ON COLUMN "DAMGEUN"."MESSAGE"."ROOMNO" IS '채팅방번호';
   COMMENT ON COLUMN "DAMGEUN"."MESSAGE"."NO" IS '메시지번호';
   COMMENT ON COLUMN "DAMGEUN"."MESSAGE"."MESSAGE" IS '메시지내용';
   COMMENT ON COLUMN "DAMGEUN"."MESSAGE"."IMAGEURL" IS '이미지URL';
   COMMENT ON COLUMN "DAMGEUN"."MESSAGE"."USERID" IS '보낸사람아이디';
   COMMENT ON COLUMN "DAMGEUN"."MESSAGE"."SENDTIME" IS '보낸 시간';
```

#### 상품 찜 테이블 생성
```SQL
  CREATE TABLE "DAMGEUN"."FAVORITE" 
   (	"USERNO" NUMBER(11,0) NOT NULL ENABLE, 
	"FV_NO" NUMBER(11,0) NOT NULL ENABLE, 
	"PD_NUM" NUMBER(11,0) NOT NULL ENABLE, 
	 CONSTRAINT "FAVORITE_PK" PRIMARY KEY ("USERNO", "FV_NO")
  USING INDEX PCTFREE 10 INITRANS 2 MAXTRANS 255 
  STORAGE(INITIAL 65536 NEXT 1048576 MINEXTENTS 1 MAXEXTENTS 2147483645
  PCTINCREASE 0 FREELISTS 1 FREELIST GROUPS 1 BUFFER_POOL DEFAULT FLASH_CACHE DEFAULT CELL_FLASH_CACHE DEFAULT)
  TABLESPACE "SYSTEM"  ENABLE, 
	 CONSTRAINT "USERNO_FAVORITE_FK" FOREIGN KEY ("USERNO")
	  REFERENCES "DAMGEUN"."USER_INFO" ("USERNO") ENABLE
   ) SEGMENT CREATION IMMEDIATE 
  PCTFREE 10 PCTUSED 40 INITRANS 1 MAXTRANS 255 NOCOMPRESS LOGGING
  STORAGE(INITIAL 65536 NEXT 1048576 MINEXTENTS 1 MAXEXTENTS 2147483645
  PCTINCREASE 0 FREELISTS 1 FREELIST GROUPS 1 BUFFER_POOL DEFAULT FLASH_CACHE DEFAULT CELL_FLASH_CACHE DEFAULT)
  TABLESPACE "SYSTEM";

   COMMENT ON COLUMN "DAMGEUN"."FAVORITE"."USERNO" IS '유저번호';
   COMMENT ON COLUMN "DAMGEUN"."FAVORITE"."FV_NO" IS '찜하기번호';
   COMMENT ON COLUMN "DAMGEUN"."FAVORITE"."PD_NUM" IS '상품번호';
```

#### 거래 후기 테이블 생성
```SQL
CREATE TABLE "DAMGEUN"."SALE_REVIEW" 
   (	"PD_NUM" NUMBER(11,0) NOT NULL ENABLE, 
	"USERNO" NUMBER(11,0) NOT NULL ENABLE, 
	"BUYERNO" NUMBER(11,0) NOT NULL ENABLE, 
	"REVIEW" CLOB NOT NULL ENABLE, 
	"IMAGEURL" VARCHAR2(255) NOT NULL ENABLE, 
	 CONSTRAINT "SALE_REVIEW_PK" PRIMARY KEY ("PD_NUM", "USERNO", "BUYERNO")
  USING INDEX PCTFREE 10 INITRANS 2 MAXTRANS 255 
  STORAGE(INITIAL 65536 NEXT 1048576 MINEXTENTS 1 MAXEXTENTS 2147483645
  PCTINCREASE 0 FREELISTS 1 FREELIST GROUPS 1 BUFFER_POOL DEFAULT FLASH_CACHE DEFAULT CELL_FLASH_CACHE DEFAULT)
  TABLESPACE "SYSTEM"  ENABLE, 
	 CONSTRAINT "FK_SALE_REVIEW_PRODUCT" FOREIGN KEY ("USERNO", "PD_NUM")
	  REFERENCES "DAMGEUN"."PRODUCT" ("USERNO", "PD_NUM") ENABLE
   ) SEGMENT CREATION IMMEDIATE 
  PCTFREE 10 PCTUSED 40 INITRANS 1 MAXTRANS 255 NOCOMPRESS LOGGING
  STORAGE(INITIAL 65536 NEXT 1048576 MINEXTENTS 1 MAXEXTENTS 2147483645
  PCTINCREASE 0 FREELISTS 1 FREELIST GROUPS 1 BUFFER_POOL DEFAULT FLASH_CACHE DEFAULT CELL_FLASH_CACHE DEFAULT)
  TABLESPACE "SYSTEM" 
 LOB ("REVIEW") STORE AS BASICFILE (
  TABLESPACE "SYSTEM" ENABLE STORAGE IN ROW CHUNK 8192 RETENTION 
  NOCACHE LOGGING 
  STORAGE(INITIAL 65536 NEXT 1048576 MINEXTENTS 1 MAXEXTENTS 2147483645
  PCTINCREASE 0 FREELISTS 1 FREELIST GROUPS 1 BUFFER_POOL DEFAULT FLASH_CACHE DEFAULT CELL_FLASH_CACHE DEFAULT)); 

   COMMENT ON COLUMN "DAMGEUN"."SALE_REVIEW"."PD_NUM" IS '상품번호';
   COMMENT ON COLUMN "DAMGEUN"."SALE_REVIEW"."USERNO" IS '판매자번호';
   COMMENT ON COLUMN "DAMGEUN"."SALE_REVIEW"."BUYERNO" IS '구매자번호';
   COMMENT ON COLUMN "DAMGEUN"."SALE_REVIEW"."REVIEW" IS '후기내용';
   COMMENT ON COLUMN "DAMGEUN"."SALE_REVIEW"."IMAGEURL" IS '이미지URL';
```

![[Pasted image 20250524182435.png]]


