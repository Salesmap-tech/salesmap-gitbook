# 방문자 상세 조회

## 방문자 상세 조회

`GET` `/v2/sdr/lead/{leadId}`

SeA 프로필 API 토큰이 속한 SDR 프로필의 특정 방문자 상세 정보를 조회합니다.

### 언제 사용하나요?

방문자 목록에서 받은 ID로 개인정보 동의 시각과 연결 회사를 함께 확인할 때 사용합니다.

### Headers

| Name | Value |
| --- | --- |
| Authorization | `Bearer <sea-profile-token>` |

`<sea-profile-token>`은 워크스페이스 설정 > SeA > API 메뉴에서 SDR 프로필별로 발급한 SeA 프로필 API 토큰입니다. 응답은 토큰이 속한 SDR 프로필의 데이터로 제한됩니다.

### Path parameters

| Name | Type | Description |
| --- | --- | --- |
| `leadId` | string | 방문자 ID Required |

### Response fields

| Name | Type | Description |
| --- | --- | --- |
| `lead` | object | 방문자 상세 정보 |
| `lead.id` | string | 방문자 ID |
| `lead.organizationId` | string \| null | 연결된 회사 ID |
| `lead.fieldList` | array | 방문자 필드 값 목록 |
| `lead.privacyConsentAgreedAt` | string \| null | 개인정보 동의 시각 |
| `lead.organization` | object \| null | 같은 SDR 프로필 범위의 연결 회사 요약 |
| `lead.organization.id` | string | 회사 ID |
| `lead.organization.name` | string | 회사 이름 |
| `lead.organization.segmentId` | string \| null | 세그먼트 ID |
| `lead.organization.segmentName` | string \| null | 세그먼트 이름 |

#### fieldList

| Name | Type | Description |
| --- | --- | --- |
| `id` | string | 필드 ID |
| `label` | string | 필드 이름 |
| `value` | string \| number \| boolean | 필드 값. 빈 문자열과 null 값은 응답에서 제외됩니다. |

### Request

```bash
curl -X GET 'https://app.salesmap.kr/api/v2/sdr/lead/<leadId>' \
  -H 'Authorization: Bearer <sea-profile-token>'
```

### Response

#### 200

```json
{
  "success": true,
  "data": {
    "lead": {
      "id": "lead-id",
      "organizationId": "organization-id",
      "fieldList": [{"id": "field-id", "label": "이름", "value": "홍길동"}],
      "lastVisitedAt": "2026-07-22T07:00:00.000Z",
      "contactCollected": true,
      "notedForSales": false,
      "privacyConsentAgreedAt": "2026-07-22T06:30:00.000Z",
      "organization": {
        "id": "organization-id",
        "name": "세일즈맵",
        "segmentId": "segment-id",
        "segmentName": "Enterprise"
      },
      "createdAt": "2026-07-22T06:00:00.000Z",
      "updatedAt": "2026-07-22T07:00:00.000Z"
    }
  }
}
```

#### 404

요청한 방문자가 존재하지 않거나 토큰이 속한 SDR 프로필 범위가 아니면 404가 반환됩니다.
