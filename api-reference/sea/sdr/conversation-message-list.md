# 대화 메시지 목록 조회

## 대화 메시지 목록 조회

`GET` `/v2/sdr/conversation/{conversationId}/message`

특정 대화의 메시지를 생성순으로 최대 50개 조회합니다. 생성이 완료된 메시지만 반환되며 생성 중이거나 실패한 메시지는 포함되지 않습니다.

### Headers

| Name | Value |
| --- | --- |
| Authorization | `Bearer <sea-profile-token>` |

`<sea-profile-token>`은 워크스페이스 설정 > SeA > API 메뉴에서 SDR 프로필별로 발급한 SeA 프로필 API 토큰입니다. 응답은 토큰이 속한 SDR 프로필의 데이터로 제한됩니다.

### Path parameters

| Name | Type | Description |
| --- | --- | --- |
| `conversationId` | string | 대화 ID Required |

### Query parameters

| Name | Type | Description |
| --- | --- | --- |
| `cursor` | string | 이전 응답의 `nextCursor`. 없으면 첫 페이지를 조회합니다. |

### Response fields

| Name | Type | Description |
| --- | --- | --- |
| `messageList` | array | 메시지 목록 |
| `messageList[].id` | string | 메시지 ID |
| `messageList[].conversationId` | string | 대화 ID |
| `messageList[].role` | string | `user` 또는 `assistant` |
| `messageList[].content` | string | 메시지 본문 |
| `messageList[].createdAt` | string | 생성 시각 |
| `nextCursor` | string \| null | 다음 페이지 커서. `null`이면 마지막 페이지입니다. |

### Request

```bash
curl -X GET 'https://salesmap.kr/api/v2/sdr/conversation/<conversationId>/message' \
  -H 'Authorization: Bearer <sea-profile-token>'
```

### Response

#### 200

```json
{
  "success": true,
  "data": {
    "messageList": [
      {
        "id": "message-id",
        "conversationId": "conversation-id",
        "role": "assistant",
        "content": "안녕하세요. 무엇을 도와드릴까요?",
        "createdAt": "2026-07-22T07:01:00.000Z"
      }
    ],
    "nextCursor": null
  }
}
```

#### 404

요청한 대화가 존재하지 않거나 토큰이 속한 SDR 프로필 범위가 아니면 404가 반환됩니다.
