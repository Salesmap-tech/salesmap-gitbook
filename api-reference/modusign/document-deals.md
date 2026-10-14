# 모두싸인 계약서 연결 딜 조회

## 모두싸인 계약서 연결 딜 조회

`GET` `/v2/modusign/document/{documentId}/deal`

Salesmap에 저장된 모두싸인 계약서에 연결된 딜 ID 전체를 조회합니다. `documentId`는 모두싸인 웹훅의 `document.id`이며, Salesmap 내부 계약서 ID가 아닙니다.

### 언제 사용하나요?

모두싸인 서명 완료 이벤트를 받은 뒤 연결 딜을 조회하고, 딜 상세 정보에 따라 후속 자동화를 실행할 때 사용합니다.

### Headers

| Name | Value |
| --- | --- |
| Authorization | `Bearer {token}` |

### Path parameters

| Name | Type | Description |
| --- | --- | --- |
| `documentId` | string | 모두싸인 외부 계약서 ID. Required |

### Request

```http
GET /api/v2/modusign/document/{documentId}/deal
Authorization: Bearer {token}
```

### Response

#### 200

```json
{
  "success": true,
  "data": {
    "dealIds": ["deal-id-1", "deal-id-2"]
  }
}
```

| Name | Type | Description |
| --- | --- | --- |
| `success` | boolean | 성공 여부 |
| `data.dealIds` | string[] | 같은 워크스페이스의 삭제되지 않은 연결 딜 ID. 중복 없이 ID 오름차순으로 반환 |

정상적으로 동기화된 계약서라도 연결된 딜이 없으면 `dealIds: []`를 반환합니다. 다른 워크스페이스 또는 삭제된 딜은 결과에 포함하지 않습니다.

#### 503: 최초 동기화 중

```json
{
  "success": false,
  "message": "Service Unavailable",
  "reason": "sync_pending"
}
```

`Retry-After: 60` 헤더를 반환합니다. 헤더의 초 단위 시간 이후 같은 요청을 다시 조회하세요. 이 값은 동기화 완료 예상 시간이나 완료 보장이 아닙니다.

#### 409: 최초 동기화 최종 실패

```json
{
  "success": false,
  "message": "Conflict",
  "reason": "sync_failed"
}
```

`Retry-After` 헤더는 없습니다. 자동 재시도를 중단하고 상태 확인 또는 수동 처리를 요청하세요. 이 조회 API는 동기화를 복구하지 않습니다.

### 주요 에러

| Status | 설명 | 처리 |
| --- | --- | --- |
| `404` | 없는 계약서 ID, 다른 워크스페이스의 계약서, 삭제된 계약서는 동일하게 `계약서를 찾을 수 없습니다.` 사유로 응답 | 계약서 ID와 API 토큰의 워크스페이스를 확인. 자동 재시도하지 않음 |
| `409` | `reason=sync_failed` | 자동 재시도 중단, 수동 확인 |
| `503` | `reason=sync_pending` | `Retry-After` 이후 재조회 |
| `401` / `403` | 인증 또는 권한 오류 | 인증·권한 확인 |
| `429` | 요청 한도 초과 | 요청 한도 정책에 따라 처리 |
| `500` 또는 `sync_pending`이 아닌 `503` | 서버 오류 | 동기화 상태로 해석하지 않고 별도 장애로 처리 |

### 후속 자동화 흐름

1. 모두싸인 이벤트와 `documentId`를 고객사 작업 저장소에 보존하고 웹훅에 2xx로 응답합니다. 웹훅 요청 안에서 60초 대기하지 않습니다.
2. 고객사 worker 또는 예약 작업에서 이 API를 호출합니다. `sync_pending`이면 `Retry-After` 이후 다음 실행을 예약합니다. 최초 대기 시작 시각과 고객사가 정한 대기 상한을 보존하고, 재시도마다 상한을 초기화하지 않습니다.
3. `dealIds` 전체를 사용해 [딜 단일 조회](../deal/one.md)를 호출합니다. 빈 배열은 정상 미연결이므로 알림 대상에서 제외합니다.
4. 딜 응답의 `data.deal[0]`에서 현재 워크스페이스의 필드명 키로 값을 읽습니다. 담당자는 `{id, name}` 또는 `null`이며, 사용자 정의 필드명과 타입은 워크스페이스 설정을 확인해야 합니다.
5. Slack 알림이 필요하면 고객사가 준비한 Salesmap 사용자 ID ↔ Slack 사용자 ID 매핑을 사용합니다. 이벤트 식별자(없으면 이벤트 종류와 `documentId`)와 `dealId` 기준으로 중복 알림을 방지하고 실패 기록·수동 재처리 경로를 둡니다.

딜 상세 조회 전에 딜이 삭제되면 기존 딜 API는 `400`과 `reason="딜을 찾을 수 없습니다."`를 반환합니다. 신규 계약서 조회의 `404`와 구분하세요. 필드명이 바뀌거나 값이 없는 경우도 정상 미연결과 구분해 처리하세요.
