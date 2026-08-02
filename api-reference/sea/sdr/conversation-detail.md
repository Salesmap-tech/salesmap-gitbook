# 대화 상세 조회

## 대화 상세 조회

`GET` `/v2/sdr/conversation/{conversationId}`

SeA 프로필 API 토큰이 속한 SDR 프로필의 특정 대화를 조회합니다.

### Headers

| Name | Value |
| --- | --- |
| Authorization | `Bearer <sea-profile-token>` |

`<sea-profile-token>`은 워크스페이스 설정 > SeA > API 메뉴에서 SDR 프로필별로 발급한 SeA 프로필 API 토큰입니다. 응답은 토큰이 속한 SDR 프로필의 데이터로 제한됩니다.

### Path parameters

| Name | Type | Description |
| --- | --- | --- |
| `conversationId` | string | 대화 ID Required |

### Response fields

| Name | Type | Description |
| --- | --- | --- |
| `conversation.id` | string | 대화 ID |
| `conversation.leadId` | string | 방문자 ID |
| `conversation.lastMessageAt` | string \| null | 마지막 메시지 시각 |
| `conversation.contactCollected` | boolean | 이 대화에서 연락처가 수집됐는지 여부 |
| `conversation.notedForSales` | boolean | 이 대화에서 담당자 호출이 발생했는지 여부 |
| `conversation.createdAt` | string | 생성 시각 |
| `conversation.updatedAt` | string | 수정 시각 |

### Request

```bash
curl -X GET 'https://salesmap.kr/api/v2/sdr/conversation/<conversationId>' \
  -H 'Authorization: Bearer <sea-profile-token>'
```

### Response

#### 200

```json
{
  "success": true,
  "data": {
    "conversation": {
      "id": "conversation-id",
      "leadId": "lead-id",
      "lastMessageAt": "2026-07-22T07:10:00.000Z",
      "contactCollected": true,
      "notedForSales": false,
      "createdAt": "2026-07-22T07:00:00.000Z",
      "updatedAt": "2026-07-22T07:10:00.000Z"
    }
  }
}
```

#### 404

요청한 대화가 존재하지 않거나 토큰이 속한 SDR 프로필 범위가 아니면 404가 반환됩니다.
