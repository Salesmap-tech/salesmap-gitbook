# 파일 목록 조회

## 파일 목록 조회

`GET` `/v2/file`

특정 레코드에 첨부된 파일 목록을 조회합니다.

### 언제 사용하나요?

세일즈맵 화면에서 딜, 리드, 고객 등 레코드 상세의 **첨부파일** 탭에 보이는 파일 목록을 API로 조회할 때 사용합니다.

### Headers

| Name          | Value            |
| ------------- | ---------------- |
| Authorization | `Bearer <token>` |

### Query parameters

| Name         | Type   | Description                                                       |
| ------------ | ------ | ----------------------------------------------------------------- |
| `objectType` | string | 조회할 대상의 종류 Required. 입력값은 "파일 업로드 · 첨부" 문서의 표를 참고하세요. |
| `objectId`   | string | 조회할 대상 레코드의 ID Required                                       |
| `cursor`     | string | 페이지네이션을 위한 커서. 이전 응답의 `nextCursor` 값을 입력합니다.            |

### 페이지네이션

한 번에 최대 50개를 반환합니다.

* 응답에 `nextCursor`가 **있으면** 다음 페이지가 있다는 뜻입니다. 그 값을 `cursor`에 넣어 이어서 조회합니다.
* 응답에 `nextCursor`가 **없으면** 마지막 페이지입니다. 빈 페이지를 한 번 더 조회할 필요가 없습니다.

`cursor`는 서버가 발급하는 값입니다. 직접 만들거나 수정하지 마세요. 잘못된 값을 보내면 400 에러가 발생합니다.

### Request

#### 딜에 첨부된 파일 목록 조회하기

```bash
curl -H "Authorization: Bearer <token>" \
  "https://salesmap.kr/api/v2/file?objectType=deal&objectId=<dealId>"
```

#### 다음 페이지 조회하기

이전 응답의 `nextCursor` 값을 `cursor`에 넣어 호출합니다.

```bash
curl -H "Authorization: Bearer <token>" \
  "https://salesmap.kr/api/v2/file?objectType=deal&objectId=<dealId>&cursor=<nextCursor>"
```

### Response

#### 200

```json
{
  "success": true,
  "data": {
    "fileList": [
      {
        "id": "<fileId>",
        "name": "contract.pdf",
        "createdAt": "2026-07-04T05:59:23.217Z",
        "owner": {
          "id": "<userId>",
          "name": "홍길동"
        }
      }
    ],
    "nextCursor": "<cursor>"
  }
}
```

| Name         | Type   | Description                                        |
| ------------ | ------ | -------------------------------------------------- |
| `id`         | string | 파일의 ID. 파일 삭제에 사용합니다.                       |
| `name`       | string | 원본 파일명                                            |
| `createdAt`  | string | 업로드 일시                                            |
| `owner`      | object | 업로드한 사용자(`id`, `name`). 없으면 `null`입니다.        |
| `nextCursor` | string | 다음 페이지 커서. 마지막 페이지에서는 반환되지 않습니다.       |

#### 40x

```json
{
  "success": false,
  "message": "에러 메세지"
}
```

### 주요 에러

| Status | 상황                                                        |
| ------ | ----------------------------------------------------------- |
| 400    | `objectType`·`objectId` 누락, 허용되지 않는 `objectType`, 잘못된 `cursor` |
| 401    | 인증에 실패했습니다.                                            |
| 429    | 요청 횟수 제한을 초과했습니다.                                     |
