# 필드 목록 조회

## 필드 목록 조회

`GET` `/v2/field/{type}`

고객, 회사, 딜 등 특정 대상에 설정된 데이터 필드 목록을 조회합니다.

응답에는 기본 필드와 커스텀 필드가 함께 포함됩니다. `singleSelect`, `multiSelect` 타입 필드는 선택지 목록인 `optionList`를 함께 반환합니다.

### Headers

| Name          | Value            |
| ------------- | ---------------- |
| Authorization | `Bearer <token>` |

### Path parameters

| Name   | Type   | Description            |
| ------ | ------ | ---------------------- |
| `type` | string | 필드 목록을 조회할 대상 Required |

URL의 `{type}`에는 필드를 조회할 대상을 입력합니다.

| 화면에서의 대상 | API에 입력하는 값     |
| -------- | --------------- |
| 고객       | `people`        |
| 회사       | `organization`  |
| 딜        | `deal`          |
| 리드       | `lead`          |
| 상품       | `product`       |
| 견적서      | `quote`         |
| 견적 상품    | `quote-product` |
| 할 일      | `todo`          |
| 커스텀 오브젝트 | `custom-object` |

### Response

#### 200

```json
{
  "success": true,
  "data": {
    "fieldList": [
      {
        "id": "<fieldId>",
        "name": "관심도",
        "type": "singleSelect",
        "required": false,
        "optionList": [
          {
            "id": "<optionId1>",
            "value": "높음"
          },
          {
            "id": "<optionId2>",
            "value": "낮음"
          }
        ]
      }
    ]
  }
}
```

| Name         | Type    | Description                                     |
| ------------ | ------- | ----------------------------------------------- |
| `id`         | string  | 필드 ID                                           |
| `name`       | string  | 필드 이름                                           |
| `type`       | string  | 필드 타입                                           |
| `required`   | boolean | 필수 여부                                           |
| `optionList` | array   | `singleSelect`, `multiSelect` 타입에서만 반환되는 선택지 목록 |

`optionList`의 각 항목은 아래 값을 포함합니다.

| Name    | Type   | Description |
| ------- | ------ | ----------- |
| `id`    | string | 선택지 ID      |
| `value` | string | 선택지 값       |

#### 40x

```json
{
  "success": false,
  "message": "에러 메세지"
}
```
