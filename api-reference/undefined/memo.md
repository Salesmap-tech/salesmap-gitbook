# 노트 목록 조회

<mark style="color:green;">`GET`</mark> `/v2/memo`

노트 목록을 조회합니다.

### 언제 사용하나요?

특정 딜, 고객, 회사, 리드에 남긴 노트를 확인하거나, 작성일·작성자·유형으로 필터하여 노트 목록을 조회할 때 사용합니다.

### Headers

| Name          | Value              |
| ------------- | ------------------ |
| Authorization | `Bearer <token>`   |

### Query parameters

| Name             | Type   | Description |
| ---------------- | ------ | ----------- |
| `cursor`         | string | 페이지네이션 커서. 응답의 `nextCursor` 값을 전달합니다. 선택 |
| `startDate`      | string | 작성일(createdAt) 시작 date-time (ISO 8601). 선택 |
| `endDate`        | string | 작성일(createdAt) 종료 date-time (ISO 8601). 선택 |
| `ownerId`        | string | 작성자 ID 필터 (UUID). 선택 |
| `typeId`         | string | 노트 유형 ID 필터 (UUID). `GET /v2/memo/type-list`의 `_id`. 선택 |
| `dealId`         | string | 연결된 딜 ID 필터 (UUID). 선택 |
| `leadId`         | string | 연결된 리드 ID 필터 (UUID). 선택 |
| `peopleId`       | string | 연결된 고객 ID 필터 (UUID). 선택 |
| `organizationId` | string | 연결된 회사 ID 필터 (UUID). 선택 |

### Request

#### 특정 딜에 연결된 노트 목록 조회

```bash
curl -X GET 'https://salesmap.kr/api/v2/memo?dealId=<dealId>' \
  -H 'Authorization: Bearer <token>'
```

#### 작성일 범위와 작성자로 필터

```bash
curl -X GET 'https://salesmap.kr/api/v2/memo?startDate=2026-01-01T00:00:00.000Z&endDate=2026-06-30T23:59:59.999Z&ownerId=<userId>' \
  -H 'Authorization: Bearer <token>'
```

### Response

#### 200

```json
{
    "success": true,
    "data": {
        "memoList": [
            {
                "id": "<memoId>",
                "cursorId": "<cursorId>",
                "text": "메모 내용",
                "htmlBody": "<p>메모 내용</p>",
                "typeList": [
                {
                    "_id": "<typeId>",
                    "value": "회의록",
                    "color": "blue"
                }
            ],
                "dealId": "<dealId>",
                "leadId": null,
                "peopleId": null,
                "organizationId": null,
                "productId": null,
                "quoteId": null,
                "todoId": null,
                "parentId": null,
                "ownerId": "<userId>",
                "updatedAt": "2024-04-03T05:59:23.217Z",
                "createdAt": "2024-04-03T05:59:23.217Z"
            }
        ],
        "nextCursor": "cursor"
    }
}
```

| Name | Type | Description |
| ---- | ---- | ----------- |
| `id` | string | 노트 ID |
| `cursorId` | string | 페이지네이션 커서값 |
| `text` | string | 노트 본문 (plain text) |
| `htmlBody` | string | 노트 본문 (HTML) |
| `typeList` | object[] | 노트 유형 객체 배열. 유형 미지정 시 `[]`. 각 객체: `_id`(UUID), `value`(유형명), `color`(색상명) |
| `dealId` / `leadId` / `peopleId` / `organizationId` | string\|null | 연결된 딜/리드/고객/회사 ID |
| `productId` / `quoteId` / `todoId` / `parentId` | string\|null | 연결된 상품/견적서/할 일/부모 노트 ID |
| `ownerId` | string | 작성자 ID |
| `createdAt` / `updatedAt` | string | 생성/수정 시각 (ISO 8601) |

#### 40x

```json
{
    "success": false,
    "message": "에러 메세지"
}
```

### 주요 에러

| Status | 상황 |
| ------ | ---- |
| 400    | `startDate` 또는 `endDate`가 유효하지 않은 date-time 형식입니다. |
| 401    | 인증에 실패했습니다. |
| 429    | 요청 횟수 제한을 초과했습니다. |
