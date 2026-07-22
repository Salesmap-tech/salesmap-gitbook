# 회사 상세 조회

## 회사 상세 조회

`GET` `/v2/sdr/organization/{organizationId}`

SeA 프로필 API 토큰이 속한 SDR 프로필의 특정 회사를 조회합니다.

### Headers

| Name | Value |
| --- | --- |
| Authorization | `Bearer <sea-profile-token>` |

`<sea-profile-token>`은 워크스페이스 설정 > SeA > API 메뉴에서 SDR 프로필별로 발급한 SeA 프로필 API 토큰입니다. 응답은 토큰이 속한 SDR 프로필의 데이터로 제한됩니다.

### Path parameters

| Name | Type | Description |
| --- | --- | --- |
| `organizationId` | string | 회사 ID Required |

### Response fields

| Name | Type | Description |
| --- | --- | --- |
| `organization.id` | string | 회사 ID |
| `organization.name` | string | 회사 이름 |
| `organization.segmentId` | string \| null | 세그먼트 ID |
| `organization.segmentName` | string \| null | 세그먼트 이름 |
| `organization.fieldList` | array | 회사 보강 필드 값 목록 |
| `organization.createdAt` | string | 생성 시각 |
| `organization.updatedAt` | string | 수정 시각 |

#### fieldList

| Name | Type | Description |
| --- | --- | --- |
| `id` | string | 필드 ID |
| `label` | string | 필드 이름 |
| `value` | string \| number \| boolean | 필드 값. 빈 문자열과 null 값은 응답에서 제외됩니다. |

### Request

```bash
curl -X GET 'https://app.salesmap.kr/api/v2/sdr/organization/<organizationId>' \
  -H 'Authorization: Bearer <sea-profile-token>'
```

### Response

#### 200

```json
{
  "success": true,
  "data": {
    "organization": {
      "id": "organization-id",
      "name": "세일즈맵",
      "segmentId": "segment-id",
      "segmentName": "Enterprise",
      "fieldList": [{"id": "field-id", "label": "직원 수", "value": 100}],
      "createdAt": "2026-07-22T06:00:00.000Z",
      "updatedAt": "2026-07-22T07:00:00.000Z"
    }
  }
}
```

#### 404

요청한 회사가 존재하지 않거나 토큰이 속한 SDR 프로필 범위가 아니면 404가 반환됩니다.
