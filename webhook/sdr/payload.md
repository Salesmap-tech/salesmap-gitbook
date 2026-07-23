# 웹훅 형태

SDR 웹훅은 `Content-Type: application/json` 형식으로 전송됩니다.

## Payload

| 속성 | 유형 | 필수 여부 | 설명 |
| --- | --- | --- | --- |
| `event` | string | Y | 발생한 이벤트입니다. |
| `occurredAt` | string | Y | 이벤트 발생 시각입니다. ISO 8601 형식으로 전달됩니다. |
| `sdrConfigId` | string | Y | 이벤트가 발생한 SDR 프로필 ID입니다. |
| `leadId` | string \| null | Y | 이벤트가 발생한 방문자 ID입니다. |
| `conversationId` | string \| null | Y | 이벤트가 발생한 대화 ID입니다. |

`roomId`와 회사 분류 ID는 페이로드에 포함되지 않습니다.

## 연락처 수집

```json
{
  "event": "sdr.lead.created",
  "occurredAt": "2026-07-23T02:15:30.412Z",
  "sdrConfigId": "2c9f0d3a-1bd0-4e26-9bce-0a6b4111fd76",
  "leadId": "4512f848-d5ea-4684-95d0-1eb18a415d86",
  "conversationId": "019f8a12-7d4b-7000-b79d-9472b564af20"
}
```

## 담당자 연결 요청

```json
{
  "event": "sdr.handoff.requested",
  "occurredAt": "2026-07-23T02:18:07.105Z",
  "sdrConfigId": "2c9f0d3a-1bd0-4e26-9bce-0a6b4111fd76",
  "leadId": "4512f848-d5ea-4684-95d0-1eb18a415d86",
  "conversationId": "019f8a12-7d4b-7000-b79d-9472b564af20"
}
```

## 회사 분류 식별

```json
{
  "event": "sdr.segment.identified",
  "occurredAt": "2026-07-23T02:20:44.728Z",
  "sdrConfigId": "2c9f0d3a-1bd0-4e26-9bce-0a6b4111fd76",
  "leadId": "4512f848-d5ea-4684-95d0-1eb18a415d86",
  "conversationId": "019f8a12-7d4b-7000-b79d-9472b564af20"
}
```
