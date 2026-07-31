# 방문자 목록 조회

## 방문자 목록 조회

`GET` `/v2/sdr/lead`

SeA 프로필 API 토큰이 속한 SDR 프로필의 방문자를 최신 생성순으로 최대 50개 조회합니다.

### 언제 사용하나요?

외부 CRM, 메신저, BI 도구에서 SeA가 수집한 방문자 목록을 페이지 단위로 동기화할 때 사용합니다.

### Headers

| Name | Value |
| --- | --- |
| Authorization | `Bearer <sea-profile-token>` |

`<sea-profile-token>`은 워크스페이스 설정 > SeA > API 메뉴에서 SDR 프로필별로 발급한 SeA 프로필 API 토큰입니다. 응답은 토큰이 속한 SDR 프로필의 데이터로 제한됩니다.

### Query parameters

| Name | Type | Description |
| --- | --- | --- |
| `cursor` | string | 이전 응답의 `nextCursor`. 없으면 첫 페이지를 조회합니다. |

### Response fields

| Name | Type | Description |
| --- | --- | --- |
| `leadList` | array | 방문자 목록 |
| `leadList[].id` | string | 방문자 ID |
| `leadList[].organizationId` | string \| null | 연결된 회사 ID |
| `leadList[].fieldList` | array | 방문자 필드 값 목록 |
| `leadList[].lastVisitedAt` | string \| null | 마지막 방문 시각 |
| `leadList[].contactCollected` | boolean | 연락처 수집 여부 |
| `leadList[].notedForSales` | boolean | 담당자 호출 여부 |
| `leadList[].createdAt` | string | 생성 시각 |
| `leadList[].updatedAt` | string | 수정 시각 |
| `nextCursor` | string \| null | 다음 페이지 커서. `null`이면 마지막 페이지입니다. |

#### fieldList

| Name | Type | Description |
| --- | --- | --- |
| `id` | string | 필드 ID |
| `label` | string | 필드 이름 |
| `value` | string \| number \| boolean | 필드 값. 빈 문자열과 null 값은 응답에서 제외됩니다. |

### Request

```bash
curl -X GET 'https://salesmap.kr/api/v2/sdr/lead' \
  -H 'Authorization: Bearer <sea-profile-token>'
```

### Response

#### 200

```json
{
  "success": true,
  "data": {
    "leadList": [
      {
        "id": "lead-id",
        "organizationId": "organization-id",
        "fieldList": [
          {"id": "field-id", "label": "이메일", "value": "visitor@example.com"}
        ],
        "lastVisitedAt": "2026-07-22T07:00:00.000Z",
        "contactCollected": true,
        "notedForSales": false,
        "createdAt": "2026-07-22T06:00:00.000Z",
        "updatedAt": "2026-07-22T07:00:00.000Z"
      }
    ],
    "nextCursor": null
  }
}
```
