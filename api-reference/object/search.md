# 오브젝트 검색

## 오브젝트 검색

<mark style="color:yellow;">`POST`</mark> `/v2/object/{targetType}/search`

고객, 회사, 딜, 리드 레코드를 필터 그룹으로 검색합니다. 필터 그룹 사이에는 OR, 같은 그룹 안의 필터 사이에는 AND 조건이 적용됩니다.

### 언제 사용하나요?

외부 시스템에서 CRM 레코드를 동기화하기 전에 이름, 이메일, 금액, 날짜, 선택 필드 같은 조건으로 기존 레코드를 찾아야 할 때 사용합니다. 예를 들어 이메일이 있는 고객 중 이름에 특정 문자열이 포함된 레코드나, 금액이 일정 기준 이상인 딜을 검색할 수 있습니다.

### Headers

| Name | Value |
| --- | --- |
| Content-Type | `application/json` |
| Authorization | `Bearer <token>` |

### Path parameters

| Name | Type | Description |
| --- | --- | --- |
| `targetType` | string | 검색할 오브젝트 타입. `people`, `organization`, `deal`, `lead` 중 하나만 사용할 수 있습니다. |

### Query parameters

| Name | Type | Description |
| --- | --- | --- |
| `cursor` | string | 페이지네이션 커서. 이전 응답의 `data.nextCursor` 값을 그대로 전달합니다. |

### Body parameters

| Name | Type | Description |
| --- | --- | --- |
| `filterGroupList` | array | 필수. 필터 그룹 목록입니다. 1~3개까지 입력할 수 있고, 그룹 사이에는 OR 조건이 적용됩니다. |
| `filterGroupList[].filters` | array | 필수. 한 그룹 안의 필터 목록입니다. 1~3개까지 입력할 수 있고, 필터 사이에는 AND 조건이 적용됩니다. |
| `filterGroupList[].filters[].fieldName` | string | 필수. 기본 필드 또는 데이터 필드의 이름입니다. 정확한 필드 이름은 `GET /v2/field/{type}`으로 확인합니다. |
| `filterGroupList[].filters[].operator` | string | 필수. 검색 연산자입니다. 아래 연산자 표를 참고하세요. |
| `filterGroupList[].filters[].value` | string \| number \| boolean \| array | 조건부 필수. `EXISTS`, `NOT_EXISTS`에서는 생략할 수 있고, 그 외 연산자에서는 필수입니다. 빈 문자열은 허용되지 않습니다. |

{% hint style="info" %}
고객·회사·딜·리드의 이름 필드는 모두 `이름`입니다. `고객 이름`, `회사 이름`, `딜 이름`, `리드 이름`처럼 타입명을 붙이면 유효하지 않은 필드 이름으로 처리됩니다.
{% endhint %}

### Operators

| Category | Operator | 적용 필드 타입 | Value 규칙 |
| --- | --- | --- | --- |
| 공통 | `EQ`, `NEQ` | 대부분의 필드 | 실제 필드 타입과 맞는 값을 입력합니다. |
| 존재 여부 | `EXISTS`, `NOT_EXISTS` | 대부분의 필드 | `value`를 생략합니다. |
| 문자열 | `CONTAINS`, `NOT_CONTAINS` | 텍스트 필드 | 문자열 값을 입력합니다. |
| 숫자 비교 | `LT`, `LTE`, `GT`, `GTE` | 숫자 필드 | 숫자 또는 숫자로 해석 가능한 문자열을 입력합니다. |
| 선택 | `IN`, `NOT_IN` | 단일 선택 필드 | 문자열 하나 또는 문자열 배열을 입력합니다. |
| 목록 포함 | `LIST_CONTAIN`, `LIST_NOT_CONTAIN` | 다중 선택·관계 필드 | 단일 값을 입력합니다. 관계 필드는 UUID 또는 레거시 ObjectId 형식의 RecordId를 입력합니다. |
| 날짜 | `DATE_ON_OR_AFTER`, `DATE_ON_OR_BEFORE`, `DATE_IS_SPECIFIC_DAY` | 날짜·날짜시간 필드 | 날짜 또는 날짜시간 문자열을 입력합니다. |
| 날짜 범위 | `DATE_BETWEEN` | 날짜·날짜시간 필드 | 시작일과 종료일 2개 값을 담은 배열을 입력합니다. |
| 상대 날짜 | `DATE_MORE_THAN_DAYS_AGO`, `DATE_LESS_THAN_DAYS_AGO`, `DATE_LESS_THAN_DAYS_LATER`, `DATE_MORE_THAN_DAYS_LATER`, `DATE_AGO`, `DATE_LATER` | 날짜·날짜시간 필드 | 숫자 또는 숫자로 해석 가능한 문자열을 입력합니다. |

### Request

#### 이메일이 일치하는 고객 검색

```json
{
  "filterGroupList": [
    {
      "filters": [
        {"fieldName": "이메일", "operator": "EQ", "value": "test@test.com"}
      ]
    }
  ]
}
```

#### 이메일이 있고 이름에 “테스트”가 포함된 고객 검색

```json
{
  "filterGroupList": [
    {
      "filters": [
        {"fieldName": "이메일", "operator": "EXISTS"},
        {"fieldName": "이름", "operator": "CONTAINS", "value": "테스트"}
      ]
    }
  ]
}
```

#### 명시적으로 체크 해제된 레코드 검색

```json
{
  "filterGroupList": [
    {
      "filters": [
        {"fieldName": "동의 여부", "operator": "EQ", "value": false}
      ]
    }
  ]
}
```

### Response

#### 200

```json
{
  "success": true,
  "data": {
    "objectList": [
      {"id": "<objectId>", "name": "테스트 고객"}
    ],
    "nextCursor": null
  }
}
```

| Name | Type | Description |
| --- | --- | --- |
| `data.objectList` | array | 검색 조건에 맞는 레코드 목록입니다. |
| `data.objectList[].id` | string | 레코드 ID입니다. UUID 또는 레거시 ObjectId일 수 있습니다. |
| `data.objectList[].name` | string | 레코드 표시 이름입니다. |
| `data.nextCursor` | string \| null | 다음 페이지 커서입니다. 다음 페이지가 없으면 `null`입니다. |

#### 40x

```json
{
  "success": false,
  "message": "Bad Request",
  "reason": "Invalid Parameters"
}
```

### 주요 에러

| Status | Description |
| --- | --- |
| 400 | `targetType`이 `people`, `organization`, `deal`, `lead` 중 하나가 아닙니다. |
| 400 | `filterGroupList` 또는 `filters`가 비어 있거나 최대 개수를 초과했습니다. |
| 400 | 존재하지 않는 `fieldName`을 입력했습니다. |
| 400 | 필드 타입에 맞지 않는 `operator` 또는 `value`를 입력했습니다. |
| 401 | Authorization 헤더가 없거나 토큰이 유효하지 않습니다. |
| 429 | 요청 한도를 초과했습니다. |
