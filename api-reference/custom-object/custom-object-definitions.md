# 커스텀 오브젝트 종류 조회

## 커스텀 오브젝트 종류 조회

`GET` `/v2/custom-object-definitions`

워크스페이스에 생성된 커스텀 오브젝트 종류를 조회합니다.

커스텀 오브젝트에 필드를 생성하거나 커스텀 오브젝트 데이터를 생성할 때 사용할 커스텀 오브젝트 종류의 `id`와 `name`을 확인할 수 있습니다.

### 언제 사용하나요?

커스텀 오브젝트 대상 API를 호출하기 전에, 워크스페이스에 어떤 커스텀 오브젝트 종류가 있는지 확인할 때 사용합니다.

예를 들어 "커스텀 오브젝트 1"에 필드를 만들거나 데이터를 생성하려면 먼저 이 API로 "커스텀 오브젝트 1"의 `id` 또는 `name`을 확인한 뒤, 요청의 `customObjectDefinitionId` 또는 `customObjectDefinitionName`으로 전달합니다.

### Headers

| Name          | Value            |
| ------------- | ---------------- |
| Authorization | `Bearer <token>` |

### Request

요청 본문은 없습니다.

### Response

#### 200

```json
{
  "success": true,
  "data": {
    "customObjectDefinitionList": [
      {
        "id": "<customObjectDefinitionId>",
        "name": "커스텀 오브젝트 1"
      },
      {
        "id": "<customObjectDefinitionId>",
        "name": "커스텀 오브젝트 2"
      }
    ]
  }
}
```

| Name                         | Type  | Description    |
| ---------------------------- | ----- | -------------- |
| `customObjectDefinitionList` | array | 커스텀 오브젝트 종류 목록 |

`customObjectDefinitionList`의 각 항목은 아래 값을 포함합니다.

| Name   | Type   | Description    |
| ------ | ------ | -------------- |
| `id`   | string | 커스텀 오브젝트 종류 ID |
| `name` | string | 커스텀 오브젝트 종류 이름 |

커스텀 오브젝트가 없으면 빈 배열을 반환합니다.

```json
{
  "success": true,
  "data": {
    "customObjectDefinitionList": []
  }
}
```

#### 40x

```json
{
  "success": false,
  "message": "에러 메시지"
}
```

### 주요 에러

| Status | 상황                |
| ------ | ----------------- |
| 401    | 인증에 실패했습니다.       |
| 429    | 요청 횟수 제한을 초과했습니다. |
