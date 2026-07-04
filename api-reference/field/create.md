# 필드 생성

## 필드 생성

`POST` `/v2/field/{type}`

고객, 회사, 딜 등 특정 대상에 데이터 필드를 생성합니다.

텍스트, 숫자처럼 선택지가 필요 없는 일반 필드는 `name`과 `type`만으로 생성할 수 있습니다. 커스텀 오브젝트에 필드를 만들 때는 `customObjectDefinitionId`가 필요합니다.

이 문서는 필드 자체를 생성하는 방법을 다룹니다. 고객, 회사, 딜 등 레코드에 실제 필드 값을 입력하는 방법은 각 레코드 생성/수정 API의 요청 본문을 참고해 주세요.

필드 생성에는 워크스페이스 플랜, 권한, 필드 개수 제한이 적용됩니다.

### 언제 사용하나요?

세일즈맵 화면에서 회사 설정 > 오브젝트 관리로 들어가 필드를 추가하는 것과 같은 작업을 API로 처리할 때 사용합니다.

예를 들어 고객에 "고객 코드" 텍스트 필드를 만들려면 URL의 `{type}`에는 `people`, 요청 본문의 `type`에는 `string`을 입력합니다.

### Headers

| Name          | Value              |
| ------------- | ------------------ |
| Content-Type  | `application/json` |
| Authorization | `Bearer <token>`   |

### Path parameters

| Name   | Type   | Description         |
| ------ | ------ | ------------------- |
| `type` | string | 필드를 생성할 대상 Required |

URL의 `{type}`에는 필드를 어느 대상에 만들지 입력합니다.

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

### Body parameters

| Name                       | Type    | Description                                                                           |
| -------------------------- | ------- | ------------------------------------------------------------------------------------- |
| `name`                     | string  | 생성할 필드의 이름 Required                                                                   |
| `type`                     | string  | 만들 필드의 종류 Required                                                                    |
| `customObjectDefinitionId` | string  | 커스텀 오브젝트에 필드를 만들 때 필요한 커스텀 오브젝트 정의 ID                                                 |
| `description`              | string  | 필드 설명                                                                                 |
| `categoryName`             | string  | 필드를 생성할 카테고리 이름. 생략하면 대상의 기본 카테고리에 생성됩니다.                                             |
| `showInCreateForm`         | boolean | 레코드 생성 화면에 표시할지 여부. 생략하면 `false`입니다.                                                  |
| `required`                 | boolean | 필수 입력 여부. 생략하면 `false`입니다.                                                            |
| `options`                  | array   | `singleSelect`, `multiSelect` 필드의 선택지                                                 |
| `isSensitive`              | boolean | 보안 필드 여부. 생략하면 `false`입니다.                                                            |
| `preventDuplicates`        | boolean | 같은 값이 중복으로 저장되지 않게 할지 여부. 생략하면 `false`입니다. 텍스트, 숫자 필드에서만 사용할 수 있습니다.                  |
| `formula`                  | string  | 계산 필드 수식. `formula`가 있으면 `type`은 계산 결과 타입으로 사용됩니다. 수식에서 필드는 `{{대상명.필드명}}` 형식으로 참조합니다. |

`customObjectDefinitionId`는 `GET /v2/custom-object-definitions`에서 확인할 수 있습니다.

### 생성 가능한 필드 타입

| 만들 필드        | API에 입력하는 값       |
| ------------ | ----------------- |
| 텍스트          | `string`          |
| 숫자           | `number`          |
| 날짜           | `date`            |
| 날짜 (시간)      | `dateTime`        |
| True / False | `boolean`         |
| 단일 선택        | `singleSelect`    |
| 복수 선택        | `multiSelect`     |
| 파일 (복수)      | `multiAttachment` |
| 사용자 (단일)     | `user`            |
| 사용자 (복수)     | `multiUser`       |

계산 필드는 별도 타입을 사용하지 않습니다. `formula`를 함께 보내면 계산 필드로 생성되며, `type`은 계산 결과 타입을 의미합니다.

### 계산 필드 생성

계산 필드는 요청 본문에 `formula`를 함께 보내서 생성합니다.

계산 필드를 만들 때 `type`은 필드 종류가 아니라 **계산 결과 타입**을 의미합니다. 예를 들어 계산 결과가 숫자이면 `type`에 `number`를 입력합니다.

```json
{
  "name": "총 계약 금액",
  "type": "number",
  "formula": "{{딜.수량}} * {{딜.단가}}"
}
```

위 요청은 딜의 `수량` 필드와 `단가` 필드를 곱해 `총 계약 금액`을 계산하는 숫자 타입 계산 필드를 생성합니다.

계산 필드에서 참조할 필드는 `{{대상명.필드명}}` 형식으로 입력합니다.

계산 필드의 결과 타입으로 사용할 수 있는 값은 아래와 같습니다.

| 계산 결과        | API에 입력하는 값 |
| ------------ | ----------- |
| 텍스트          | `string`    |
| 숫자           | `number`    |
| 날짜           | `date`      |
| 날짜 (시간)      | `dateTime`  |
| True / False | `boolean`   |

### 생성 제약

* `singleSelect`는 `options`를 1개 이상 입력해야 합니다.
* `multiSelect`는 `options`를 2개 이상 입력해야 합니다.
* 선택지의 `value`는 같은 필드 안에서 중복될 수 없습니다.
* `required`를 `true`로 설정하려면 `showInCreateForm`도 `true`로 설정해야 합니다.
* `isSensitive`와 `preventDuplicates`는 함께 사용할 수 없습니다.
* `preventDuplicates`는 `string`, `number` 타입에서만 사용할 수 있습니다.
* `isSensitive`는 `string`, `number`, `date`, `dateTime`, `boolean`, `singleSelect`, `multiSelect` 타입에서만 사용할 수 있습니다.
* `quote-product`, `todo` 대상에는 `multiAttachment` 필드를 생성할 수 없습니다.
* `customObjectDefinitionId`는 `custom-object` 대상에서만 사용할 수 있습니다.
* `categoryName`은 해당 대상에 존재하는 카테고리 이름이어야 합니다.

계산 필드는 아래 제약을 따릅니다.

* 계산 필드의 결과 타입은 `string`, `number`, `date`, `dateTime`, `boolean`만 사용할 수 있습니다.
* `formula`를 보내면 `options`, `showInCreateForm`, `required`, `isSensitive`, `preventDuplicates`를 함께 설정할 수 없습니다.

### 선택지 입력 구조

`singleSelect`, `multiSelect`에서만 사용합니다.

```json
{
  "options": [
    {"value": "VIP"},
    {"value": "일반"}
  ]
}
```

| Name    | Type   | Description     |
| ------- | ------ | --------------- |
| `value` | string | 선택지 이름 Required |

### Request

#### 고객에 "고객 코드" 텍스트 필드 만들기

고객을 내부 코드로 구분할 수 있도록 텍스트 필드를 추가합니다.

```json
{
  "name": "고객 코드",
  "type": "string"
}
```

#### 고객에 "관심도" 단일 선택 필드 만들기

고객별 관심도를 "높음", "낮음" 중 하나로 선택할 수 있는 필드를 추가합니다.

```json
{
  "name": "관심도",
  "type": "singleSelect",
  "options": [
    {"value": "높음"},
    {"value": "낮음"}
  ]
}
```

#### 딜에 "계약 유형" 필드 만들기

딜을 계약 유형별로 구분할 수 있도록 텍스트 필드를 추가합니다. `categoryName`을 입력하면 해당 카테고리에 필드가 생성됩니다.

```json
{
  "name": "계약 유형",
  "type": "string",
  "categoryName": "기본 정보"
}
```

#### 딜에 "총 계약 금액" 계산 필드 만들기

딜의 수량과 단가를 이용해 총 계약 금액을 자동으로 계산하는 필드를 추가합니다.

```json
{
  "name": "총 계약 금액",
  "type": "number",
  "formula": "{{딜.수량}} * {{딜.단가}}"
}
```

#### 커스텀 오브젝트에 "중요도" 필드 만들기

특정 커스텀 오브젝트에 중요도를 기록할 수 있는 텍스트 필드를 추가합니다.

```json
{
  "customObjectDefinitionId": "custom-object-definition-id",
  "name": "중요도",
  "type": "string"
}
```

### Response

#### 201

```json
{
  "success": true,
  "data": {
    "field": {
      "id": "<fieldId>",
      "name": "관심도",
      "type": "singleSelect",
      "showInCreateForm": false,
      "required": false,
      "isSensitive": false,
      "preventDuplicates": false,
      "options": [
        {"id": "<optionId1>", "value": "높음"},
        {"id": "<optionId2>", "value": "낮음"}
      ],
      "createdAt": "2026-05-12T00:00:00.000Z"
    }
  }
}
```

| Name                | Type    | Description                  |
| ------------------- | ------- | ---------------------------- |
| `id`                | string  | 생성된 필드 ID                    |
| `name`              | string  | 필드 이름                        |
| `type`              | string  | 필드 타입. 계산 필드에서는 계산 결과 타입입니다. |
| `formula`           | string  | 계산 필드일 때 반환되는 수식             |
| `description`       | string  | 필드 설명                        |
| `showInCreateForm`  | boolean | 레코드 생성 화면 표시 여부              |
| `required`          | boolean | 필수 입력 여부                     |
| `isSensitive`       | boolean | 보안 필드 여부                     |
| `preventDuplicates` | boolean | 중복 방지 여부                     |
| `options`           | array   | 선택 필드일 때 반환되는 선택지 목록         |
| `createdAt`         | string  | 필드 생성 일시                     |

계산 필드 응답에서는 `type`이 계산 결과 타입을 의미하며, `formula`를 함께 반환합니다.

```json
{
  "success": true,
  "data": {
    "field": {
      "id": "<fieldId>",
      "name": "총 계약 금액",
      "type": "number",
      "formula": "{{딜.수량}} * {{딜.단가}}",
      "showInCreateForm": false,
      "required": false,
      "isSensitive": false,
      "preventDuplicates": false,
      "createdAt": "2026-05-12T00:00:00.000Z"
    }
  }
}
```

#### 40x

```json
{
  "success": false,
  "message": "에러 메세지"
}
```

### 주요 에러

| Status | 상황                                          |
| ------ | ------------------------------------------- |
| 400    | 요청 형식이 올바르지 않거나, 지원하지 않는 필드 타입 조합입니다.       |
| 401    | 인증에 실패했습니다.                                 |
| 403    | 플랜 또는 권한 제한으로 필드를 생성할 수 없습니다.               |
| 404    | 필드를 만들 대상, 커스텀 오브젝트 정의, 필드 카테고리를 찾을 수 없습니다. |
| 409    | 같은 이름의 필드가 이미 존재합니다.                        |
| 429    | 요청 횟수 제한을 초과했습니다.                           |
