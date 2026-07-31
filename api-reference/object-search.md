# 오브젝트 검색

<mark style="color:yellow;">`POST`</mark> `/v2/object/{targetType}/search`

고객, 회사, 딜, 리드를 복합 조건으로 검색합니다. 필터 그룹끼리는 OR, 한 그룹 안의 필터끼리는 AND로 결합됩니다.

**Headers**

| Name          | Value              |
| ------------- | ------------------ |
| Content-Type  | `application/json` |
| Authorization | `Bearer <token>`   |

**Path and query parameters**

| Name         | Type   | Description |
| ------------ | ------ | ----------- |
| `targetType` | string | 검색 대상. `people`, `organization`, `deal`, `lead` 중 하나 <br><mark style="color:red;"><strong>Required</strong></mark> |
| `cursor`     | string | 다음 페이지 커서 |

**Body parameters**

| Name                          | Type                                   | Description |
| ----------------------------- | -------------------------------------- | ----------- |
| `filterGroupList`             | array                                  | 필터 그룹. 1개 이상 3개 이하 <br><mark style="color:red;"><strong>Required</strong></mark> |
| `filterGroupList[].filters`   | array                                  | 그룹 안의 필터. 1개 이상 3개 이하 <br><mark style="color:red;"><strong>Required</strong></mark> |
| `filters[].fieldName`         | string                                 | 검색할 필드 이름 <br><mark style="color:red;"><strong>Required</strong></mark> |
| `filters[].operator`          | string                                 | 검색 연산자 <br><mark style="color:red;"><strong>Required</strong></mark> |
| `filters[].value`             | string, number, boolean, string[]       | 비교할 값. `EXISTS`, `NOT_EXISTS` 외에는 필수이며 연산자와 실제 필드 타입에 맞아야 함 |

지원 연산자는 다음과 같습니다.

* 공통: `EQ`, `NEQ`, `EXISTS`, `NOT_EXISTS`
* 문자열: `CONTAINS`, `NOT_CONTAINS`
* 숫자: `LT`, `LTE`, `GT`, `GTE`. JSON number 외에 십진수·지수·16진수(`0x`)·2진수(`0b`)·8진수(`0o`) 문자열도 사용할 수 있습니다.
* 선택·관계: `IN`, `NOT_IN`, `LIST_CONTAIN`, `LIST_NOT_CONTAIN`. `IN`, `NOT_IN`은 문자열 또는 비어 있지 않은 문자열 배열을 사용합니다. `LIST_CONTAIN`, `LIST_NOT_CONTAIN`은 다중 선택 및 관계 필드에서 단일 문자열을 사용하며, 관계 필드에는 UUID 또는 레거시 ObjectId 형식의 단일 RecordId를 전달합니다.
* 날짜: `DATE_ON_OR_AFTER`, `DATE_ON_OR_BEFORE`, `DATE_IS_SPECIFIC_DAY`, `DATE_BETWEEN`, `DATE_MORE_THAN_DAYS_AGO`, `DATE_LESS_THAN_DAYS_AGO`, `DATE_LESS_THAN_DAYS_LATER`, `DATE_MORE_THAN_DAYS_LATER`, `DATE_AGO`, `DATE_LATER`

`DATE_BETWEEN`은 유효한 날짜 문자열 두 개로 이루어진 배열을 사용합니다. 나머지 지정일 연산자는 날짜 문자열 하나를, 오늘 기준 경과일 연산자는 숫자를 사용합니다. 날짜시간은 `T` 또는 공백으로 날짜와 시간을 구분할 수 있고 타임존은 선택 사항입니다(예: `2026-01-01T09:30:00`, `2026-01-01 09:30`). `EQ`, `NEQ`의 값 타입은 대상 필드에 따라 문자열, 숫자 또는 boolean입니다.

**Request**

```json
{
  "filterGroupList": [
    {
      "filters": [
        { "fieldName": "이메일", "operator": "EXISTS" },
        { "fieldName": "이름", "operator": "CONTAINS", "value": "김" }
      ]
    }
  ]
}
```

**Response**

{% tabs %}
{% tab title="200" %}
```json
{
  "success": true,
  "data": {
    "objectList": [
      { "id": "<objectId>", "name": "김세일" }
    ],
    "nextCursor": null
  }
}
```
{% endtab %}

{% tab title="40x" %}
```json
{
  "success": false,
  "message": "에러 메시지"
}
```
{% endtab %}
{% endtabs %}
