# 커스텀 오브젝트 데이터 생성

## 커스텀 오브젝트 데이터 생성

`POST` `/v2/custom-object`

커스텀 오브젝트에 실제 데이터를 생성합니다.

예를 들어 "커스텀 오브젝트 1"이라는 커스텀 오브젝트 종류가 있다면, 이 API로 그 안에 새 데이터를 추가할 수 있습니다.

### 언제 사용하나요?

외부 시스템에서 세일즈맵의 커스텀 오브젝트에 데이터를 등록할 때 사용합니다.

데이터를 생성하려면 `customObjectDefinitionId` 또는 `customObjectDefinitionName`이 필요합니다. 커스텀 오브젝트 종류의 `id`와 `name`은 `GET /v2/custom-object-definitions`에서 확인할 수 있습니다.

### Headers

| Name          | Value              |
| ------------- | ------------------ |
| Content-Type  | `application/json` |
| Authorization | `Bearer <token>`   |

### Body parameters

| Name                         | Type   | Description                                 |
| ---------------------------- | ------ | ------------------------------------------- |
| `customObjectDefinitionId`   | string | 데이터를 생성할 커스텀 오브젝트 종류 ID                     |
| `customObjectDefinitionName` | string | 데이터를 생성할 커스텀 오브젝트 종류 이름                     |
| `fieldList`                  | array  | 커스텀 오브젝트의 필드 값 목록. 생성하려면 대표 필드 값을 포함해야 합니다. |
| `pipelineId`                 | string | 파이프라인 단계와 함께 지정할 파이프라인 ID                   |
| `pipelineStageId`            | string | 파이프라인과 함께 지정할 파이프라인 단계 ID                   |
| `memo`                       | string | 데이터 생성과 함께 남길 메모                            |

`customObjectDefinitionId`와 `customObjectDefinitionName` 중 하나만 입력해도 됩니다. 둘 다 입력하면 두 값이 같은 커스텀 오브젝트 종류를 가리켜야 합니다.

`pipelineId`와 `pipelineStageId`는 함께 입력해야 합니다.

### 필드 값 입력 구조

`fieldList`에는 값을 입력할 필드 이름과 값을 함께 전달합니다.

```json
{
  "fieldList": [
    {
      "name": "이름",
      "stringValue": "샘플 데이터"
    }
  ]
}
```

필드 타입에 따라 사용하는 값 필드가 다릅니다.

| 필드 타입         | 값 필드                      |
| ------------- | ------------------------- |
| 텍스트           | `stringValue`             |
| 숫자            | `numberValue`             |
| 날짜, 날짜 (시간)   | `dateValue`               |
| True / False  | `booleanValue`            |
| 단일 선택         | `stringValue`             |
| 복수 선택         | `stringValueList`         |
| 사용자           | `userValueId`             |
| 사용자 (복수)      | `userValueIdList`         |
| 고객            | `peopleValueId`           |
| 고객 (복수)       | `peopleValueIdList`       |
| 회사            | `organizationValueId`     |
| 회사 (복수)       | `organizationValueIdList` |
| 딜             | `dealValueId`             |
| 딜 (복수)        | `dealValueIdList`         |
| 리드            | `leadValueId`             |
| 리드 (복수)       | `leadValueIdList`         |
| 커스텀 오브젝트      | `customObjectValueId`     |
| 커스텀 오브젝트 (복수) | `customObjectValueIdList` |

대표 필드는 반드시 입력해야 합니다. 대표 필드는 커스텀 오브젝트 데이터의 이름으로 사용됩니다.

### Request

#### "커스텀 오브젝트 1"에 새 데이터 만들기

```json
{
  "customObjectDefinitionName": "커스텀 오브젝트 1",
  "fieldList": [
    {
      "name": "이름",
      "stringValue": "샘플 데이터"
    }
  ]
}
```

#### ID로 커스텀 오브젝트 종류를 지정해 데이터 만들기

```json
{
  "customObjectDefinitionId": "<customObjectDefinitionId>",
  "fieldList": [
    {
      "name": "이름",
      "stringValue": "샘플 데이터"
    }
  ]
}
```

#### 파이프라인 단계와 메모를 함께 입력하기

```json
{
  "customObjectDefinitionName": "커스텀 오브젝트 1",
  "pipelineId": "<pipelineId>",
  "pipelineStageId": "<pipelineStageId>",
  "memo": "외부 시스템에서 생성한 데이터입니다.",
  "fieldList": [
    {
      "name": "이름",
      "stringValue": "샘플 데이터"
    }
  ]
}
```

### Response

#### 201

```json
{
  "success": true,
  "data": {
    "customObject": {
      "id": "<customObjectId>",
      "name": "샘플 데이터",
      "createdAt": "2026-06-02T00:00:00.000Z"
    }
  }
}
```

| Name        | Type   | Description         |
| ----------- | ------ | ------------------- |
| `id`        | string | 생성된 커스텀 오브젝트 데이터 ID |
| `name`      | string | 생성된 커스텀 오브젝트 데이터 이름 |
| `createdAt` | string | 생성 일시               |

#### 40x

```json
{
  "success": false,
  "message": "에러 메시지"
}
```

### 주요 에러

| Status | 상황                                             |
| ------ | ---------------------------------------------- |
| 400    | 요청 값이 올바르지 않거나 필수 필드 값이 없습니다.                  |
| 401    | 인증에 실패했습니다.                                    |
| 404    | 입력한 커스텀 오브젝트 종류, 필드, 담당자, 파이프라인 단계를 찾을 수 없습니다. |
| 429    | 요청 횟수 제한을 초과했습니다.                              |
