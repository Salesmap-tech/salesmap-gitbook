# 커스텀 오브젝트 데이터 조회

## 커스텀 오브젝트 데이터 조회

`GET` `/v2/custom-object`

커스텀 오브젝트에 등록된 실제 데이터 목록을 조회합니다.

예를 들어 워크스페이스에 "커스텀 오브젝트 1"이라는 커스텀 오브젝트 종류가 있고, 그 안에 여러 데이터가 등록되어 있다면 이 API로 해당 데이터를 조회할 수 있습니다.

### 언제 사용하나요?

특정 커스텀 오브젝트 종류에 등록된 데이터를 외부 시스템에서 가져올 때 사용합니다.

`customObjectDefinitionId` 또는 `customObjectDefinitionName`을 입력하면 특정 커스텀 오브젝트 종류의 데이터만 조회합니다. 둘 다 생략하면 워크스페이스의 전체 커스텀 오브젝트 데이터를 조회합니다.

커스텀 오브젝트 종류의 `id`와 `name`은 `GET /v2/custom-object-definitions`에서 확인할 수 있습니다.

### Headers

| Name          | Value            |
| ------------- | ---------------- |
| Authorization | `Bearer <token>` |

### Query parameters

| Name                         | Type   | Description           |
| ---------------------------- | ------ | --------------------- |
| `cursor`                     | string | 다음 페이지를 조회할 때 사용하는 커서 |
| `customObjectDefinitionId`   | string | 조회할 커스텀 오브젝트 종류 ID    |
| `customObjectDefinitionName` | string | 조회할 커스텀 오브젝트 종류 이름    |

`customObjectDefinitionId`와 `customObjectDefinitionName` 중 하나만 입력해도 됩니다. 둘 다 입력하면 두 값이 같은 커스텀 오브젝트 종류를 가리켜야 합니다.

### Request

#### "커스텀 오브젝트 1"의 데이터 조회하기

```http
GET /v2/custom-object?customObjectDefinitionName=커스텀%20오브젝트%201
```

#### 커서로 다음 페이지 조회하기

```http
GET /v2/custom-object?customObjectDefinitionName=커스텀%20오브젝트%201&cursor=<nextCursor>
```

### Response

#### 200

```json
{
  "success": true,
  "data": {
    "customObjectList": [
      {
        "id": "<customObjectId>",
        "customObjectDefinitionId": "<customObjectDefinitionId>",
        "이름": "샘플 데이터",
        "담당자": {
          "id": "<userId>",
          "name": "홍길동"
        },
        "파이프라인": {
          "id": "<pipelineId>",
          "name": "기본 파이프라인"
        },
        "파이프라인 단계": {
          "id": "<pipelineStageId>",
          "name": "진행 중"
        }
      }
    ],
    "nextCursor": "<nextCursor>"
  }
}
```

| Name               | Type           | Description                               |
| ------------------ | -------------- | ----------------------------------------- |
| `customObjectList` | array          | 커스텀 오브젝트 데이터 목록                           |
| `nextCursor`       | string \| null | 다음 페이지 조회에 사용할 커서. 다음 페이지가 없으면 `null`입니다. |

`customObjectList`의 각 항목은 아래 값을 포함합니다.

| Name                       | Type                                                   | Description              |
| -------------------------- | ------------------------------------------------------ | ------------------------ |
| `id`                       | string                                                 | 커스텀 오브젝트 데이터 ID          |
| `customObjectDefinitionId` | string                                                 | 이 데이터가 속한 커스텀 오브젝트 종류 ID |
| `<필드 이름>`                  | string \| number \| boolean \| object \| array \| null | 커스텀 오브젝트에 정의된 필드 값       |

필드 값은 필드 이름을 key로 반환합니다. 사용자, 회사, 딜, 리드, 커스텀 오브젝트 같은 참조 값은 `{id, name}` 형태로 반환합니다.

데이터가 없으면 빈 배열을 반환합니다.

```json
{
  "success": true,
  "data": {
    "customObjectList": [],
    "nextCursor": null
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

| Status | 상황                          |
| ------ | --------------------------- |
| 400    | 요청 값이 올바르지 않습니다.            |
| 401    | 인증에 실패했습니다.                 |
| 404    | 입력한 커스텀 오브젝트 종류를 찾을 수 없습니다. |
| 429    | 요청 횟수 제한을 초과했습니다.           |
