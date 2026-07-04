# 파일 업로드 · 첨부

## 파일 업로드 · 첨부

`POST` `/v2/file`

파일을 업로드합니다. `objectType`과 `objectId`를 함께 보내면 해당 레코드에 파일이 첨부됩니다.

`objectType`과 `objectId` 없이 업로드하면 파일만 업로드됩니다. 이때 응답의 `id`를 이메일 발송 API(`POST /v2/email`)의 `attachmentIdList`에 넣어 이메일 첨부에 사용할 수 있습니다.

### 언제 사용하나요?

세일즈맵 화면에서 딜, 리드, 고객 등 레코드 상세의 **첨부파일** 탭에 파일을 올리는 것과 같은 작업을 API로 처리할 때 사용합니다.

예를 들어 특정 딜에 계약서 PDF를 첨부하려면 `objectType`에 `deal`, `objectId`에 해당 딜의 ID를 입력합니다.

### Headers

| Name          | Value                 |
| ------------- | --------------------- |
| Content-Type  | `multipart/form-data` |
| Authorization | `Bearer <token>`      |

요청 본문은 JSON이 아니라 `multipart/form-data`입니다. JSON으로 보내면 400 에러가 발생합니다.

### Body parameters (form-data)

| Name         | Type   | Description                                          |
| ------------ | ------ | ---------------------------------------------------- |
| `file`       | binary | 업로드할 파일 Required. 요청당 1개                       |
| `objectType` | string | 첨부할 대상의 종류. `objectId`와 함께 사용                 |
| `objectId`   | string | 첨부할 대상 레코드의 ID. `objectType`과 함께 사용          |

`objectType`에는 파일을 어느 대상에 첨부할지 입력합니다.

| 화면에서의 대상 | API에 입력하는 값  |
| -------- | -------------- |
| 딜        | `deal`         |
| 리드       | `lead`         |
| 고객       | `people`       |
| 회사       | `organization` |
| 상품       | `product`      |
| 견적서      | `quote`        |
| 커스텀 오브젝트 | `customObject` |
| 노트       | `memo`         |

커스텀 오브젝트에 첨부할 때 `objectId`에는 커스텀 오브젝트 **레코드**의 ID를 입력합니다. 정의(definition) ID가 아닙니다.

### 업로드 제약

* 파일 크기는 1개당 25MB 이하여야 합니다.
* 허용된 MIME 타입만 업로드할 수 있습니다: `image/jpeg` `image/png` `image/gif` `image/webp` `application/pdf` `application/zip` doc/docx/xls/xlsx/ppt/pptx `text/plain` `text/csv`
* 파일 확장자와 MIME 타입이 일치해야 합니다.
* 빈 파일(0 byte)은 업로드할 수 없습니다.
* `objectType`과 `objectId`는 반드시 함께 보내야 합니다. 한쪽만 보내면 400 에러가 발생합니다.
* 존재하지 않거나 다른 워크스페이스에 속한 레코드에는 첨부할 수 없습니다.

### Request

#### 파일만 업로드하기 (이메일 첨부용)

응답의 `id`를 이메일 발송 API의 `attachmentIdList`에 사용합니다.

```bash
curl -X POST \
  -H "Authorization: Bearer <token>" \
  -F "file=@/path/to/contract.pdf" \
  "https://salesmap.kr/api/v2/file"
```

#### 딜에 파일 첨부하기

업로드와 동시에 특정 딜의 첨부파일 탭에 파일이 첨부됩니다.

```bash
curl -X POST \
  -H "Authorization: Bearer <token>" \
  -F "file=@/path/to/contract.pdf" \
  -F "objectType=deal" \
  -F "objectId=<dealId>" \
  "https://salesmap.kr/api/v2/file"
```

### Response

#### 201

```json
{
  "success": true,
  "data": {
    "id": "<fileId>",
    "name": "contract.pdf"
  }
}
```

| Name   | Type   | Description                                              |
| ------ | ------ | -------------------------------------------------------- |
| `id`   | string | 업로드된 파일의 ID. 이메일 첨부, 파일 삭제에 사용합니다.        |
| `name` | string | 원본 파일명                                                 |

응답 형태는 `objectType` 유무와 관계없이 동일합니다.

#### 40x

```json
{
  "success": false,
  "message": "에러 메세지"
}
```

### 주요 에러

| Status | 상황                                                                          |
| ------ | --------------------------------------------------------------------------- |
| 400    | `file` 필드 누락, JSON 본문 전송, 허용되지 않는 MIME 타입, 25MB 초과, `objectType`·`objectId` 중 한쪽만 전달 |
| 401    | 인증에 실패했습니다.                                                              |
| 404    | 첨부할 대상 레코드를 찾을 수 없습니다.                                                |
| 429    | 요청 횟수 제한을 초과했습니다.                                                       |
