| 인터페이스 | 타입 | 설명 | 비고 |
| --- | --- | --- | --- |
| id | | |
## User

| **Interface**   |  **User**        | | |
------|---|---|---|
| **id** | number | unique | user 테이블의 고유 인덱스. 모든 user는 한 테이블에 저장되며, 고유의 id를 가집니다. |
| **token_id** |   number   | unique | 토큰 식별자 값을 외래키로 가집니다. |
| **nickname**   | string | x | 유저가 우리 앱에서 설정한 닉네임입니다. |


---
Category: User

| **API Name**   |  **Get User Token**        |
------|---|
| **설명** | 카카오에서 받은 인가코드를 서버에 전하고 JWT와 기존 회원 여부를 반환합니다. |
| **Method** | GET      |  
| **Path**   | /auth/kakao/callback |
| **Params**  |  code(required, 프론트에서 카카오 로그인시 받은 인가코드)  |
| **Request**   | none |   
| **Response**   | {accessToken:string(JWT), refreshToken:string(JWT), first:boolean} |
| **Auth**   | none |

| **API Name**   |  **Post Re-issuance User Token**        |
------|---|
| **설명** | 리프레쉬 토큰은 유효하나 액세스 토큰이 만료되었을 때, 액세스 토큰을 재발급합니다. |
| **Method** |    POST    |  
| **Path**   |  /api/v1/tokens/re-issuance  |
| **Params**  |  none  |
| **Request**   | none |   
| **Response**   | accessToken, refreshToken, isFirst(true일 경우 처음 회원가입한 회원) |
| **Auth**   | required |


| **API Name**   |  **Get User**        |
------|---|
| **설명** | 현재 유저의 정보를 취득합니다. |
| **Method** |    GET    |  
| **Path**   |  /api/v1/user |
| **Params**  |  none  |
| **Request**   | none |   
| **Response**   | User |
| **Auth**   | required |

| **API Name**   |  **Put User**        |
------|---|
| **설명** | 유저 정보를 수정합니다. |
| **Method** |    PUT    |  
| **Path**   |  /api/v1/user |
| **Params**  |  none  |
| **Request**   | User `수정할 항목만 보내도 OK. 예) {nickname : abc} / token_id는 수정 불가`  |   
| **Response**   | User |
| **Auth**   | required |



## Todo

| **Interface**   |  **Todo**        | |
|------|---|---|
| **id** | number | todo 테이블의 고유 인덱스. 모든 Todo는 한 테이블에 저장되며, 고유의 id를 가집니다. |
| **task** |   string   | 유저가 입력한 Todo 내용입니다. |
| **timer**   |  number | 유저가 해당 항목에서 타이머를 재생시킨 시간입니다. <br> 단위는 초입니다. | 
| **date**  |   string    | 유저가 프론트 상에서 어느 날짜 페이지에 해당 항목을 작성했는지 가리키는 인덱스입니다. <br> 유저의 실제 해당 항목 작성 시간과 일치하지 않을 수 있습니다. <br> 형식은 "YYYY-MM-DD"입니다. | 
| **isDone**   | boolean | 유저의 해당 항목에 대한 완료 상태를 나타냅니다. |   
| **createdAt**   | date | todo 항목이 만들어진 실제 시간입니다.  |   
| **updatedAt**   | date | todo 항목이 최근에 수정된 시간입니다. |   


---
Category: Todo

| **API Name**   |  **Get Todo**        |
|------|---|
| **설명** | 요청을 보낸 유저의 모든 todo list를 가져옵니다. <br> 날짜가 지정되면 해당 날짜의 todolist만 가져옵니다. |
| **Method** | GET      |  
| **Path**   | /api/v1/todo |
| **Params**  |   date(optional, string("YYYY-MM-DD"))     |
| **Request**   | none |   
| **Response**   | Todo[] |
| **Auth**   | required |

| **API Name**   |  **Update Todo**        |
|------|---|
| **설명** | 해당 Todo를 수정합니다. |
| **Method** | PUT      |  
| **Path**   | /api/v1/todo/{todo-id} |
| **Params**  |  none | 
| **Request**   | Todo |   
| **Response**   | 수정된 Todo |
| **Auth**   | required |

| **API Name**   |  **Create Todo**        |
|------|---|
| **설명** | Todo 항목을 신규 등록합니다. | 
| **Method** |   POST    |  
| **Path**   | /api/v1/todo |
| **Params**  |  none | 
| **Request**   | Todo |   
| **Response**   | {id: number;}  `todo의 등록을 완료하고 테이블에서 생성된 todo의 id를 돌려줍니다.` |
| **Auth**   | required |

| **API Name**   |  **Delete Todo**        |
|------|---|
| **설명** | 해당 Todo를 삭제합니다. |
| **Method** |  DELETE    |  
| **Path**   | /api/v1/todo/{todo-id} |
| **Params**  |  none | 
| **Request**   | none |   
| **Response**   | none |
| **Auth**   | required |

| **API Name**   |  **Get Todo Length**  |
|------|---|
| **설명** | Todo가 저장된 인덱스 날짜들의 갯수를 돌려줍니다. |
| **Method** |  GET   |  
| **Path**   | /api/v1/todo/registeredDate |
| **Params**  |  none | 
| **Request**   | none |   
| **Response**   | none |
| **Auth**   | required |



## Receipt

| **Interface**   |  **Recipt**        |    |
|------|---|---|
| **id** | number | Recipt 테이블의 고유 인덱스. 이 테이블의 영수증들은 모든 영수증이 아니라 한번이라도 핀 된 영수증을 모아두는 테이블입니다. |
| **todos** | Todo[] | 영수증을 핀했을 때의 todo 목록입니다. 외래키로 참조하지 않으며, 이 테이블에 한번 기록된 todo 항목은 내용이 수정되지 않아야 합니다. |
| **pinned** |   bool   | 현재 핀의 상태를 표시합니다.  |
| **famous_saying**   |  string | 영수증과 함께 만들어진 명언입니다. | 
| **receipt_name**  |   string    | 유저가 영수증을 핀했을 당시의 유저 닉네임입니다. 이 항목에 저장된 유저 닉네임과 현재 유저 닉네임이 다를 수 있습니다. | 
| **createdAt**   | date | 이 영수증 항목이 만들어진 실제 시간입니다.  |   
| **updatedAt**   | date | 이 영수증 항목이 최근에 수정된 시간입니다. |   


---
Category: Receipt

| **API Name**   |  **Get Pinned Receipts**        |
|------|---|
| **설명** | 해당 유저의 핀 된 영수증 목록을 돌려줍니다.  <br> `pinned`가 `true`인 항목만 돌려줍니다. |
| **Method** |   GET    |  
| **Path**   | /api/v1/receipt/pinned |
| **Params**  |  none |
| **Request**   | none |   
| **Response**   | Receipt[] |
| **Auth**   | required |

| **API Name**   |  **Post Pinned Receipt**        |
|------|---|
| **설명** | 영수증을 등록합니다. |
| **Method** |   POST    |  
| **Path**   | /api/v1/receipt/pinned |
| **Params**  |  none |
| **Request**   | body: Receipt |   
| **Response**   | {id: number;}  `receipt의 등록을 완료하고 테이블에서 생성된 receipt의 id를 돌려줍니다.`  |
| **Auth**   | required |

| **API Name**   |  **Put Pinned Receipt**        |
|------|---|
| **설명** | 영수증을 수정합니다. |
| **Method** |   PUT    |  
| **Path**   | /api/v1/receipt/pinned/id |
| **Params**  |  none |
| **Request**   | body: Receipt `수정할 항목만 보내도 OK. 예) {pinned : false}` |   
| **Response**   | Receipt |
| **Auth**   | required |


- 23.08.04 수정 내용 : API 이름의 메소드 명 표기방법 통일
