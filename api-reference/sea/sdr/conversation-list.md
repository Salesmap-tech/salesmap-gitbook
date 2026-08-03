# 대화 목록 조회

## 대화 목록 조회

`GET` `/v2/sdr/conversation`

SeA 프로필 API 토큰이 속한 SDR 프로필의 대화를 생성일 역순으로 최대 50개 조회합니다.

### 언제 사용하나요?

외부 시스템에서 SeA 대화 목록을 주기적으로 동기화할 때 사용합니다.

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
| `conversationList` | array | 대화 목록 |
| `conversationList[].id` | string | 대화 ID |
| `conversationList[].leadId` | string | 방문자 ID |
| `conversationList[].lastMessageAt` | string \| null | 마지막 메시지 시각 |
| `conversationList[].contactCollected` | boolean | 이 대화에서 연락처가 수집됐는지 여부 |
| `conversationList[].notedForSales` | boolean | 이 대화에서 담당자 호출이 발생했는지 여부 |
| `conversationList[].createdAt` | string | 생성 시각 |
| `conversationList[].updatedAt` | string | 수정 시각 |
| `nextCursor` | string \| null | 다음 페이지 커서. `null`이면 마지막 페이지입니다. |

### Request

```bash
curl -X GET 'https://salesmap.kr/api/v2/sdr/conversation' \
  -H 'Authorization: Bearer <sea-profile-token>'
```

### Response

#### 200

```json
{
  "success": true,
  "data": {
    "conversationList": [
      {
        "id": "conversation-id",
        "leadId": "lead-id",
        "lastMessageAt": "2026-07-22T07:10:00.000Z",
        "contactCollected": true,
        "notedForSales": false,
        "createdAt": "2026-07-22T07:00:00.000Z",
        "updatedAt": "2026-07-22T07:10:00.000Z"
      }
    ],
    "nextCursor": null
  }
}
```
