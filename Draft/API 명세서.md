
## User
| Interface | Type | Unique | Description |
| --------- | ---- | ------ | ----------- |
|           |      |        |             |
|           |      |        |             |

## Stamp
| Interface | Type                              | Unique | Description |
| --------- | --------------------------------- | ------ | ----------- |
| id        | number                            | true   | 스탬프의 순서     |
| img_src   | string                            |        | 이미지의 URL    |
| type      | "thumbnail" \| "none" \| "reward" |        |             |


## Sets

| Interface   | Type     |     | Description       |
| ----------- | -------- | --- | ----------------- |
| id          | number   |     | 세트의 고유한 아이디       |
| stamps      | stamp[]  |     | 스탬프 이미지 정보가 담긴 배열 |
| board       | board    |     | 스탬프 판의 정보         |
| uploader_id |          |     |                   |
| tags        | string[] |     |                   |
|             |          |     |                   |
| createdAt   | date     |     | 이 세트가 만들어진 시간입니다. |
|             |          |     |                   |

| API Name     | Get Set              | 비고  |
| ------------ | -------------------- | --- |
| Description  | 단일 세트의 정보를 조회합니다.    |     |
| Method       | GET                  |     |
| Path         | /api/v1/set/{set-id} |     |
| URL Params   | set-id               |     |
| Query Params | none                 |     |
| Request      | none                 |     |
| Response     | Set                  |     |
| Auth         | none                 |     |

| API Name     | Get Sets          | 비고  |
| ------------ | ----------------- | --- |
| Description  | 모든 세트의 정보를 조회합니다. |     |
| Method       | GET               |     |
| Path         | /api/v1/set       |     |
| URL Params   | none              |     |
| Query Parmas | none              |     |
| Request      | none              |     |
| Response     | Set[]             |     |
| Auth         | none              |     |

| API Name     | Start Rally                | 비고  |
| ------------ | -------------------------- | --- |
| Description  | 랠리를 등록합니다.                 |     |
| Method       | POST                       |     |
| Path         | /api/v1/rally              |     |
| URL Params   | none                       |     |
| Query Parmas | none                       |     |
| Request      | Set, goal, goal_detail<br> |     |
| Response     | Rally                      |     |
| Auth         | required                   |     |

| API Name     | Update Rally        | 비고  |
| ------------ | ------------------- | --- |
| Description  | 랠리의 진행상황을 업데이트 합니다. |     |
| Method       | PUT                 |     |
| Path         | /api/v1/rally       |     |
| URL Params   | none                |     |
| Query Parmas | none                |     |
| Request      | Set, progress<br>   |     |
| Response     | Rally               |     |
| Auth         | required            |     |

| API Name     | Get Rallies               | 비고  |
| ------------ | ------------------------- | --- |
| Description  | 유저가 가지고 있는 모든 랠리들을 반환합니다. |     |
| Method       | GET                       |     |
| Path         | /api/v1/rally             |     |
| URL Params   | none                      |     |
| Query Parmas | none                      |     |
| Request      | Set, progress<br>         |     |
| Response     | Rally                     |     |
| Auth         | required                  |     |
