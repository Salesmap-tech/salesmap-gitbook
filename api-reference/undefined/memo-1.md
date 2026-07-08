# 노트 단일 조회

<mark style="color:green;">`GET`</mark> `/v2/memo/<memoId>`

단일 노트를 조회합니다.

### 언제 사용하나요?

특정 노트의 상세 정보(본문, 유형, 연결 대상 등)를 조회할 때 사용합니다.

### Headers

| Name          | Value              |
| ------------- | ------------------ |
| Authorization | `Bearer <token>`   |

### Path parameters

| Name     | Type   | Description  |
| -------- | ------ | ------------ |
| `memoId` | string | 조회하려는 노트의 ID. Required |

### Request

#### 노트 단일 조회

```bash
curl -X GET 'https://salesmap.kr/api/v2/memo/<memoId>' \
  -H 'Authorization: Bearer <token>'
```

### Response

#### 200

```json
{
    "success": true,
    "data": {
        "memo": {
            "id": "<memoId>",
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
    }
}
```

| Name | Type | Description |
| ---- | ---- | ----------- |
| `id` | string | 노트 ID |
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
| 400    | 존재하지 않는 노트 ID이거나 UUID 형식이 아닙니다. (`노트를 찾을 수 없습니다.`) |
| 401    | 인증에 실패했습니다. |
| 429    | 요청 횟수 제한을 초과했습니다. |
