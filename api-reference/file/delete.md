# 파일 삭제

## 파일 삭제

`POST` `/v2/file/{fileId}/delete`

특정 파일을 삭제합니다. 요청 본문은 필요하지 않습니다.

요청한 워크스페이스에 속한 파일 중, **레코드에 첨부된 파일** 또는 **이 API로 업로드한 파일**만 삭제할 수 있습니다. 그 외의 파일(이메일 첨부, 문서, 커스텀 필드에 저장된 파일 등)은 삭제할 수 없으며 404를 반환합니다.

### 언제 사용하나요?

세일즈맵 화면에서 레코드 상세의 **첨부파일** 탭에서 파일을 삭제하는 것과 같은 작업을 API로 처리할 때 사용합니다.

삭제할 파일의 ID는 파일 업로드 응답의 `id` 또는 파일 목록 조회 응답의 `id`에서 확인할 수 있습니다.

### Headers

| Name          | Value            |
| ------------- | ---------------- |
| Authorization | `Bearer <token>` |

### Path parameters

| Name     | Type   | Description           |
| -------- | ------ | --------------------- |
| `fileId` | string | 삭제할 파일의 ID Required |

### Request

```bash
curl -X POST \
  -H "Authorization: Bearer <token>" \
  "https://salesmap.kr/api/v2/file/<fileId>/delete"
```

### Response

#### 200

```json
{
  "success": true
}
```

#### 40x

```json
{
  "success": false,
  "message": "에러 메세지"
}
```

### 주요 에러

| Status | 상황                                                   |
| ------ | ------------------------------------------------------ |
| 401    | 인증에 실패했습니다.                                       |
| 404    | 파일을 찾을 수 없거나, 다른 워크스페이스에 속하거나, 이 API로 삭제할 수 없는 파일(이메일·문서·커스텀 필드 첨부 등)입니다. |
| 429    | 요청 횟수 제한을 초과했습니다.                                |
