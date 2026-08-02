# 회사 목록 조회

## 회사 목록 조회

`GET` `/v2/sdr/organization`

SeA 프로필 API 토큰이 속한 SDR 프로필의 회사를 최신 생성순으로 최대 50개 조회합니다.

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
| `organizationList` | array | 회사 목록 |
| `organizationList[].id` | string | 회사 ID |
| `organizationList[].name` | string | 회사 이름 |
| `organizationList[].segmentId` | string \| null | 세그먼트 ID |
| `organizationList[].segmentName` | string \| null | 세그먼트 이름 |
| `organizationList[].fieldList` | array | 회사 보강 필드 값 목록 |
| `organizationList[].createdAt` | string | 생성 시각 |
| `organizationList[].updatedAt` | string | 수정 시각 |
| `nextCursor` | string \| null | 다음 페이지 커서. `null`이면 마지막 페이지입니다. |

#### fieldList

| Name | Type | Description |
| --- | --- | --- |
| `id` | string | 필드 ID |
| `label` | string | 필드 이름 |
| `value` | string \| number \| boolean | 필드 값. 빈 문자열과 null 값은 응답에서 제외됩니다. |

### Request

```bash
curl -X GET 'https://salesmap.kr/api/v2/sdr/organization' \
  -H 'Authorization: Bearer <sea-profile-token>'
```

### Response

#### 200

```json
{
  "success": true,
  "data": {
    "organizationList": [
      {
        "id": "organization-id",
        "name": "세일즈맵",
        "segmentId": "segment-id",
        "segmentName": "Enterprise",
        "fieldList": [{"id": "field-id", "label": "산업", "value": "SaaS"}],
        "createdAt": "2026-07-22T06:00:00.000Z",
        "updatedAt": "2026-07-22T07:00:00.000Z"
      }
    ],
    "nextCursor": null
  }
}
```
