---
description: 세일즈맵 MCP 서버가 제공하는 26개 도구의 상세 스펙입니다.
---

# 도구 목록

{% hint style="info" %}
AI는 대화 맥락에 따라 적절한 도구를 자동으로 선택합니다. 이 문서는 어떤 도구가 있는지 이해하고, 원하는 작업이 가능한지 확인하는 용도입니다.
{% endhint %}

### 스키마 탐색

#### salesmap-list-objects

오브젝트 목록을 조회합니다. 기본 오브젝트(고객·회사·리드·딜·상품·견적서)와 커스텀 오브젝트 모두를 포함합니다.

**사용 예시**: "우리 워크스페이스에 어떤 커스텀 오브젝트가 있어?"

#### salesmap-list-properties

오브젝트의 필드 스키마(이름·유형·옵션)을 조회합니다.

| 파라미터         | 타입   | 필수 | 설명                                                                             |
| ------------ | ---- | -- | ------------------------------------------------------------------------------ |
| `objectType` | enum | ✅  | `deal` `lead` `people` `organization` `product` `quote` `todo` `custom-object` |

**사용 예시:** “딜 오브젝트에 어떤 필드가 있는지 알려줘”

#### salesmap-create-property

필드를 생성합니다.

| 파라미터                       | 타입      | 필수     | 설명                                                                                                           |
| -------------------------- | ------- | ------ | ------------------------------------------------------------------------------------------------------------ |
| `objectType`               | enum    | ✅      | `people` `organization` `deal` `lead` `product` `quote` `quote-product` `todo` `custom-object`               |
| `customObjectDefinitionId` | string  | 조건부 필수 | `objectType`이 `custom-object` 일 경우 커스텀 오브젝트의 ID                                                              |
| `name`                     | string  | ✅      | 필드 이름                                                                                                        |
| `type`                     | enum    | ✅      | `string` `number` `date` `dateTime` `boolean` `singleSelect` `multiSelectmultiAttachment` `user` `multiUser` |
| `options`                  | array   | 조건부 필수 | `type`이 `singleSelect`·`multiSelect`일 때의 선택지 목록                                                              |
| `description`              | string  |        | 필드 설명                                                                                                        |
| `preventDuplicates`        | boolean |        | 같은 값이 중복 등록되지 않도록 막는 유니크 필드로 설정. 사업자등록번호·전화번호·프로젝트ID처럼 값이 고유해야 하는 필드에 사용 (기본 false)                          |
| `required`                 | boolean |        | 생성 모달 UI에서 입력 장제 여부 (기본 false)                                                                               |
| `showInCreateForm`         | boolean |        | 생성 모달 UI에 표시 여부 (기본 false)                                                                                   |
| `formula`                  | string  |        | 계산 수식. 입력 시 계산 유형 필드가 되며 `type`은 계산 결과의 타입이 됨                                                                |

**사용 예시:** “티켓 오브젝트에 중요도 필드 추가해줘"

***

### 레코드 검색

#### salesmap-search-objects

필터 조건으로 레코드를 검색합니다. 필터 그룹 간 OR, 그룹 내 필터 간 AND로 동작합니다.

| 파라미터           | 타입     | 필수 | 설명                                    |
| -------------- | ------ | -- | ------------------------------------- |
| `objectType`   | enum   | ✅  | `people` `organization` `deal` `lead` |
| `filterGroups` | array  | ✅  | 필터 그룹 배열 (최대 3개 그룹, 그룹당 최대 3개 필터)     |
| `after`        | string |    | 페이지네이션 커서                             |

**필터 객체 구조:**

| 필드             | 타입                            | 설명               |
| -------------- | ----------------------------- | ---------------- |
| `propertyName` | string                        | 필드 이름            |
| `operator`     | enum                          | 비교 연산자 (아래 표 참조) |
| `value`        | string \| number \| string\[] | 검색 값             |

<details>

<summary>지원 연산자 목록</summary>

| 연산자                                 | 설명               |
| ----------------------------------- | ---------------- |
| `EQ`                                | 같음               |
| `NEQ`                               | 같지 않음            |
| `EXISTS`                            | 값 있음             |
| `NOT_EXISTS`                        | 값 없음             |
| `CONTAINS`                          | 포함               |
| `NOT_CONTAINS`                      | 포함하지 않음          |
| `LT` / `LTE`                        | 미만 / 이하          |
| `GT` / `GTE`                        | 초과 / 이상          |
| `IN` / `NOT_IN`                     | 목록에 포함 / 불포함     |
| `LIST_CONTAIN` / `LIST_NOT_CONTAIN` | 리스트 필드에 포함 / 불포함 |
| `DATE_ON_OR_AFTER`                  | 이후 날짜            |
| `DATE_ON_OR_BEFORE`                 | 이전 날짜            |
| `DATE_IS_SPECIFIC_DAY`              | 특정 날짜            |
| `DATE_BETWEEN`                      | 날짜 범위            |
| `DATE_MORE_THAN_DAYS_AGO`           | N일 이전보다 오래됨      |
| `DATE_LESS_THAN_DAYS_AGO`           | N일 이내            |
| `DATE_LESS_THAN_DAYS_LATER`         | 앞으로 N일 이내        |
| `DATE_MORE_THAN_DAYS_LATER`         | 앞으로 N일 이후        |
| `DATE_AGO`                          | N일 전             |
| `DATE_LATER`                        | N일 후             |

</details>

**사용 예시:** “이번 달 생성된 딜 중 상태가 Won인 것 검색해줘”

***

### 레코드 목록 조회

웹 폼, 시퀀스, 상품 목록 조회만 지원합니다.

고객, 회사, 리드, 딜 등 조회는 salesmap-search-objects를 사용합니다.

#### salesmap-list-webforms

웹 폼 목록을 조회합니다.

| 파라미터    | 타입                  | 설명        |
| ------- | ------------------- | --------- |
| `after` | `string` (optional) | 페이지네이션 커서 |

#### salesmap-list-sequences

시퀀스 목록을 조회합니다.

| 파라미터    | 타입                  | 설명        |
| ------- | ------------------- | --------- |
| `after` | `string` (optional) | 페이지네이션 커서 |

#### salesmap-list-product

상품 목록을 조회합니다.

| 파라미터    | 타입                  | 설명        |
| ------- | ------------------- | --------- |
| `after` | `string` (optional) | 페이지네이션 커서 |

### 레코드 CRUD

#### salesmap-batch-read-objects

여러 레코드를 한 번에 조회합니다 (최대 20개).

| 파라미터         | 타입        | 필수 | 설명                                                                                                                                             |
| ------------ | --------- | -- | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| `objectType` | enum      | ✅  | <p><code>people</code> <code>organization</code> <code>deal</code> <code>lead</code> <code>custom-object</code></p><p><code>product</code></p> |
| `objectIds`  | string\[] | ✅  | 레코드 ID 배열 (1\~20개)                                                                                                                             |
| `properties` | string\[] |    | 반환할 필드 이름 목록. 생략 시 기본 필드 반환. 다건 조회 시 지정 권장.                                                                                                    |

#### salesmap-create-object

새 레코드를 생성합니다.

| 파라미터                       | 타입     | 필수     | 설명                                                                  |
| -------------------------- | ------ | ------ | ------------------------------------------------------------------- |
| `objectType`               | enum   | ✅      | `people` `organization` `deal` `lead` `custom-object` `product`     |
| `properties`               | object |        | <p>필드 key-value<br>예: <code>{ "이름": "홍길동", "금액": 50000 }</code></p> |
| `note`                     | string |        | 초기 메모                                                               |
| `peopleId`                 | string | 조건부 필수 | 연결할 고객 ID                                                           |
| `organizationId`           | string | 조건부 필수 | 연결할 회사 ID                                                           |
| `customObjectDefinitionId` | string | 조건부 필수 | Definition ID (custom-object 필수)                                    |

{% hint style="info" %}
딜/리드 생성 시 `peopleId` 또는 `organizationId` 중 하나 이상 필요합니다.\
딜 생성 시 `pipelineId`, `pipelineStageId`는 `salesmap_get_pipeline_ids`로 확인하세요.
{% endhint %}

#### salesmap-update-object

기존 레코드를 수정합니다.

| 파라미터             | 타입     | 필수 | 설명                                                    |
| ---------------- | ------ | -- | ----------------------------------------------------- |
| `objectType`     | enum   | ✅  | `people` `organization` `deal` `lead` `custom-object` |
| `objectId`       | string | ✅  | 레코드 ID                                                |
| `properties`     | object |    | 변경할 필드 key-value                                      |
| `peopleId`       | string |    | 연결 고객 변경                                              |
| `organizationId` | string |    | 연결 회사 변경                                              |

#### salesmap-delete-object

기존 레코드를 삭제합니다.

| 파라미터         | 타입      | 필수 | 설명                     |
| ------------ | ------- | -- | ---------------------- |
| `objectType` | enum    | ✅  | `deal` `lead`          |
| `objectId`   | string  | ✅  | 레코드 ID                 |
| `comfirmed`  | boolean |    | false=미리보기, true=실제 삭제 |

***

### 관계 조회

#### salesmap-list-associations

레코드에 연결된 다른 레코드들을 조회합니다.

| 파라미터           | 타입     | 필수 | 설명                                                           |
| -------------- | ------ | -- | ------------------------------------------------------------ |
| `objectType`   | enum   | ✅  | `people` `organization` `deal` `lead` `custom-object` `note` |
| `objectId`     | string | ✅  | 출발 레코드 ID                                                    |
| `toObjectType` | enum   | ✅  | 도착 레코드 ID                                                    |

**사용 예시:** “이 회사에 연결된 딜 목록 보여줘”

### 활동 이력

#### salesmap-list-changelog

레코드의 필드 변경 이력을 조회합니다.

| 파라미터         | 타입       | 필수 | 설명                                    |
| ------------ | -------- | -- | ------------------------------------- |
| `objectType` | `enum`   | ✅  | `people` `organization` `deal` `lead` |
| `objectId`   | `string` | ✅  | 레코드 ID                                |
| `after`      | `string` |    | 페이지네이션 커서                             |

### 노트·견적서

#### salesmap-read-note

노트(메모)의 상세 내용을 조회합니다.

| 파라미터     | 타입     | 필수 | 설명      |
| -------- | ------ | -- | ------- |
| `noteId` | string | ✅  | 노트 UUID |

#### salesmap-create-note

레코드에 노트(메모)를 추가합니다.

| 파라미터         | 타입     | 필수 | 설명                                                    |
| ------------ | ------ | -- | ----------------------------------------------------- |
| `objectType` | enum   | ✅  | `people` `organization` `deal` `lead` `custom-object` |
| `objectId`   | string | ✅  | 대상 레코드 ID                                             |
| `note`       | string | ✅  | 노트 내용                                                 |

#### salesmap-get-quotes

딜/리드에 연결된 견적서 목록을 조회합니다.

| 파라미터        | 타입     | 필수 | 설명            |
| ----------- | ------ | -- | ------------- |
| `obectType` | enum   | ✅  | `deal` `lead` |
| `objectId`  | string | ✅  | 딜/리드 ID       |

#### salesmap-create-quote

견적서를 생성합니다. `dealId` 또는 `leadId` 중 하나를 지정해야 합니다.

| 파라미터               | 타입      | 필수     | 설명        |
| ------------------ | ------- | ------ | --------- |
| `name`             | string  | ✅      | 견적서 이름    |
| `dealId`           | string  | 조건부 필수 | 연결할 딜 ID  |
| `leadId`           | string  | 조건부 필수 | 연결할 리드 ID |
| `note`             | string  |        | 노트        |
| `isMainQuote`      | boolean |        | 메인 견적서 여부 |
| `quoteProductList` | array   |        | 상품 목록     |
| `properties`       | object  |        | 커스텀 필드    |

#### salesmap-list-engagements

레코드의 활동 타임라인을 조회합니다. (이메일·노트·TODO·웹폼·미팅 등)

<table><thead><tr><th>파라미터</th><th width="249">타입</th><th>필수</th><th>설명</th></tr></thead><tbody><tr><td><code>objectType</code></td><td><code>enum</code> </td><td>✅</td><td><code>people</code> <code>organization</code> <code>deal</code> <code>lead</code></td></tr><tr><td><code>objectId</code></td><td><code>string</code></td><td>✅</td><td>레코드 ID</td></tr><tr><td><code>after</code></td><td><code>string</code></td><td></td><td>페이지네이션 커서</td></tr></tbody></table>

### 파이프라인·분석

#### salesmap-get-pipelines

파이프라인 목록과 각 단계의 ID를 조회합니다. 딜·리드 생성/검색 시 필요합니다.

| 파라미터         | 타입   | 필수 | 설명            |
| ------------ | ---- | -- | ------------- |
| `objectType` | enum | ✅  | `deal` `lead` |

#### salesmap-get-lead-time

딜/리드의 파이프라인 단계 별 체류 시간을 분석합니다.

| 파라미터         | 타입     | 필수 | 설명            |
| ------------ | ------ | -- | ------------- |
| `objectType` | enum   | ✅  | `deal` `lead` |
| `objectId`   | string | ✅  | 레코드 ID        |

**사용 예시:** “이 딜이 각 단계에서 며칠씩 걸렸는지 분석해줘”

### 유틸리티

#### salesmap-get-docs

세일즈맵 MCP의 도메인 지식을 조회합니다.

#### salesmap-report-feedback

세일즈맵 MCP의 버그·부족한 기능·개선 요청을 개발팀에 전달합니다.

| 파라미터       | 타입     | 필수 | 설명                                                                  |
| ---------- | ------ | -- | ------------------------------------------------------------------- |
| `category` | enum   | ✅  | `bug` `missing-tool` `tool-limitation` `friction` `feature-request` |
| `summary`  | string | ✅  | 한 줄 요약                                                              |
| `detail`   | string | ✅  | 무엇을 하려 했고 왜 막혔는지                                                    |

#### salesmap-get-link

레코드의 세일즈맵 웹 URL을 생성합니다.

| 파라미터         | 타입     | 필수 | 설명                                                                      |
| ------------ | ------ | -- | ----------------------------------------------------------------------- |
| `objectType` | enum   | ✅  | `people` `organization` `deal` `lead` `custom-object` `product` `quote` |
| `objectId`   | string | ✅  | 레코드 ID                                                                  |

#### salesmap-list-users

CRM 사용자 목록을 조회합니다. 담당자 지정·변경 시 필요합니다.

| 파라미터    | 타입     | 필수 | 설명        |
| ------- | ------ | -- | --------- |
| `after` | string |    | 페이지네이션 커서 |

#### salesmap-list-teams

팀 목록 + 소속 멤버를 조회합니다.

| 파라미터    | 타입     | 필수 | 설명        |
| ------- | ------ | -- | --------- |
| `after` | string |    | 페이지네이션 커서 |

#### salesmap-get-user-details

현재 API 키 소유자의 정보를 조회합니다.

***

### 도구 권한

| 구분     | 도구 수 | 해당 도구                                                                                                                                                                                                                                                                                   |
| ------ | ---- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **읽기** | 16개  | list-objects, list-properties, search-objects, batch-read-objects, list-associations, list-engagements, list-changelog, read-note, get-quotes, get-pipelines, get-lead-time, get-link, list-users, list-teams, get-user-details, get-docs, list-products, list-sequences, list-webforms |
| **쓰기** | 6개   | salesmap-create-property, create-object, update-object, create-note, create-quote, report-feedback                                                                                                                                                                                      |
| **삭제** | 1개   | delete-object                                                                                                                                                                                                                                                                           |
