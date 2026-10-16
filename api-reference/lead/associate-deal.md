# 리드·딜 연결 추가

## 리드·딜 연결 추가

`POST` `/v2/lead/{leadId}/deal/{dealId}`

`POST` `/v2/deal/{dealId}/lead/{leadId}`

두 주소는 같은 동작을 제공합니다. 기존 리드의 **딜 목록**과 기존 딜의 **리드 목록**에 서로를 추가합니다.

### 언제 사용하나요?

기존 리드와 딜을 연결하되, 양쪽의 다른 연결은 유지하고 싶을 때 사용합니다. 새 리드나 딜을 생성하는 API는 아닙니다.

### Headers

| Name | Value |
| --- | --- |
| Authorization | `Bearer {token}` |
| Idempotency-Key | 선택. 요청 경로별로 적용되는 멱등성 키 |

### Path parameters

| Name | Type | Description |
| --- | --- | --- |
| `leadId` | string | 연결할 리드 ID. Required |
| `dealId` | string | 연결할 딜 ID. Required |

두 레코드 모두 인증된 워크스페이스에 속해야 합니다. 다른 워크스페이스의 ID는 존재하지 않는 ID와 동일하게 처리합니다.

### Request

요청 본문과 쿼리 파라미터는 필요하지 않습니다.

```http
POST /v2/lead/{leadId}/deal/{dealId}
Authorization: Bearer {token}
```

### 연결 처리 규칙

- 양쪽의 기존 연결을 유지하면서 지정한 연결을 추가합니다.
- 양쪽에 이미 연결되어 있으면 변경 이력이나 워크플로를 추가하지 않고 성공합니다.
- 한쪽 연결만 빠져 있으면 해당 쪽만 추가합니다.
- 관계 설정의 연결 개수 제한을 저장 전에 검사합니다.
- 관계 저장과 후속 작업 예약을 처리한 뒤 응답합니다. 집계·검색 동기화·워크플로의 실행 완료까지 기다리지는 않습니다.
- 처리 중 실패하면 일부 관계나 후속 작업이 이미 반영되었을 수 있습니다. 재호출이 누락된 모든 후속 작업을 복구하는 것은 아닙니다.
- 두 주소를 번갈아 호출해도 같은 연결을 처리하지만, `Idempotency-Key`의 캐시는 요청 경로별로 적용됩니다.

### Response

#### 200

연결 처리에 성공했거나 양쪽에 이미 연결된 경우입니다.

```json
{
  "success": true,
  "data": {
    "leadId": "{leadId}",
    "dealId": "{dealId}"
  }
}
```

| Name | Type | Description |
| --- | --- | --- |
| `success` | boolean | 성공 시 `true` |
| `data.leadId` | string | 연결한 리드 ID |
| `data.dealId` | string | 연결한 딜 ID |

### 주요 에러

| Status | 설명 |
| --- | --- |
| 400 | 관계 설정의 연결 개수 제한 초과 등 잘못된 요청 |
| 401 | 인증 실패 |
| 403 | API 접근 권한 또는 플랜 제한 |
| 404 | 리드 또는 딜이 없거나 인증된 워크스페이스에 속하지 않음 |
| 429 | 요청 제한 초과 |
| 500 | 처리 중 서버 오류. 일부 반영 가능성은 위 연결 처리 규칙 참고 |

404 응답의 메시지는 대상에 따라 `연결할 리드를 찾을 수 없습니다.` 또는 `연결할 딜을 찾을 수 없습니다.`입니다.
