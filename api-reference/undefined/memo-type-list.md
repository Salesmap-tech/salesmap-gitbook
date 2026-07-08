# 노트 유형 목록 조회

<mark style="color:green;">`GET`</mark> `/v2/memo/type-list`

워크스페이스에 설정된 노트 유형 전체를 조회합니다.

### 언제 사용하나요?

노트 작성 UI의 유형 드롭다운을 채우거나, `GET /v2/memo`의 `typeId` 필터에 쓸 id를 얻을 때 사용합니다. 유형 id(`_id`)를 알아야 특정 유형의 노트만 필터링할 수 있습니다.

### Headers

| Name          | Value              |
| ------------- | ------------------ |
| Authorization | `Bearer <token>`   |

### Request

#### 노트 유형 목록 조회

```bash
curl -X GET 'https://salesmap.kr/api/v2/memo/type-list' \
  -H 'Authorization: Bearer <token>'
```

### Response

#### 200

```json
{
    "success": true,
    "data": {
        "typeList": [
            {
                "_id": "<typeId>",
                "value": "회의록",
                "color": "blue"
            },
            {
                "_id": "<typeId>",
                "value": "고객 미팅",
                "color": "orange"
            }
        ]
    }
}
```

| Name | Type | Description |
| ---- | ---- | ----------- |
| `_id` | string | 유형 ID (UUID). `GET /v2/memo?typeId=` 필터에 사용합니다. Required |
| `value` | string | 유형 이름. Required |
| `color` | string | 유형 색상 이름 (예: `blue`, `orange`, `lime`, `pink`). hex 코드가 아닙니다. Required |

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
| 401    | 인증에 실패했습니다. |
| 429    | 요청 횟수 제한을 초과했습니다. |
