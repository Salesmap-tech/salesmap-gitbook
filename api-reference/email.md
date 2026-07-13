# 이메일 발송 및 조회

## 이메일 발송

`POST` `/v2/email`

세일즈맵에 연동된 메일 계정으로 이메일을 발송합니다.

Gmail, Outlook, 마케팅 이메일, IMAP, POP3 발송 계정을 사용할 수 있습니다. 첨부 파일은 먼저 파일 업로드 API로 업로드한 뒤 `attachmentIdList` 또는 `inlineAttachmentIdList`에 전달합니다.

### 언제 사용하나요?

외부 시스템에서 세일즈맵 사용자의 연동 메일 계정을 통해 고객에게 이메일을 보내고, 발송 결과의 이메일 ID와 메시지 ID를 저장해야 할 때 사용합니다.

### Headers

| Name          | Value              |
| ------------- | ------------------ |
| Content-Type  | `application/json` |
| Authorization | `Bearer <token>`   |

### Body parameters

| Name                     | Type   | Description |
| ------------------------ | ------ | ----------- |
| `emailProvider`          | string | 발송 계정 종류 Required. `gmail`, `outlook`, `marketingEmail`, `imap`, `pop3` 중 하나입니다. |
| `fromAddress`            | object | 발신자 표시 이름 또는 발신 이메일을 지정할 때 사용합니다. |
| `fromAddress.name`       | string | 발신자 표시 이름. 생략하면 요청 사용자의 이름을 사용합니다. |
| `fromAddress.email`      | string | 발신 이메일 주소. provider별로 허용된 주소만 사용할 수 있습니다. |
| `toAddressList`          | array  | 수신자 목록 Required. 최소 1명 이상 필요합니다. |
| `toAddressList[].name`   | string | 수신자 이름 |
| `toAddressList[].email`  | string | 수신자 이메일 Required |
| `ccAddressList`          | array  | 참조 수신자 목록 |
| `bccAddressList`         | array  | 숨은 참조 수신자 목록 |
| `subject`                | string | 제목 Required |
| `htmlBody`               | string | HTML 본문 Required |
| `attachmentIdList`       | array  | 일반 첨부 파일 ID 목록. `POST /v2/file`로 업로드한 파일 ID를 전달합니다. |
| `inlineAttachmentIdList` | array  | 본문 inline 이미지로 사용할 첨부 파일 ID 목록 |
| `inReplyTo`              | string | 답장으로 묶을 원본 이메일의 Message-ID |

### 발신자 선택 규칙

`emailProvider`별로 발신 주소가 결정되는 방식이 다릅니다.

| emailProvider | 발신 주소 규칙 |
| ------------- | -------------- |
| `gmail` | 기본 Gmail 주소를 사용합니다. `fromAddress.email`을 지정하면 Gmail send-as alias에 등록된 주소여야 합니다. |
| `outlook` | Outlook 연동 주소를 사용합니다. `fromAddress.email`을 지정하면 연동 주소와 같아야 합니다. |
| `marketingEmail` | 워크스페이스의 마케팅 이메일 도메인을 사용합니다. 보이는 From 주소는 항상 상위 마케팅 도메인(`marketingEmailDomain`)으로 계산됩니다. SES Custom MAIL FROM 서브도메인은 envelope-from 용도이며 보이는 From 주소에 사용되지 않습니다. |
| `imap`, `pop3` | 해당 IMAP/POP3 연동 주소를 사용합니다. `fromAddress.email`을 지정하면 연동 주소와 같아야 합니다. |

`marketingEmail`에서 `fromAddress.email`을 지정할 경우, 값은 `사용자 이메일의 local-part + @ + 워크스페이스 마케팅 이메일 도메인` 형태여야 합니다. 예를 들어 사용자 이메일이 `user@example.com`이고 워크스페이스 마케팅 이메일 도메인이 `salesmap.kr`이면 허용되는 발신 주소는 `user@salesmap.kr`입니다.

### Request

#### 마케팅 이메일 계정으로 발송하기

```json
{
  "emailProvider": "marketingEmail",
  "fromAddress": {
    "name": "Salesmap Team"
  },
  "toAddressList": [
    {"name": "홍길동", "email": "hong@example.com"}
  ],
  "subject": "안녕하세요",
  "htmlBody": "<p>세일즈맵에서 발송한 이메일입니다.</p>"
}
```

#### 첨부 파일과 함께 발송하기

```json
{
  "emailProvider": "gmail",
  "toAddressList": [
    {"email": "customer@example.com"}
  ],
  "subject": "자료 전달드립니다",
  "htmlBody": "<p>첨부 파일을 확인해주세요.</p>",
  "attachmentIdList": ["<fileId>"]
}
```

### Response

#### 201

```json
{
  "success": true,
  "data": {
    "id": "<emailId>",
    "messageId": "<messageId>"
  }
}
```

| Name        | Type   | Description |
| ----------- | ------ | ----------- |
| `id`        | string | 세일즈맵 이메일 ID |
| `messageId` | string | 발송된 이메일의 Message-ID. 외부 메일 서비스 재조회가 지연되는 경우 빈 문자열일 수 있습니다. |

### Error cases

| Code | Condition |
| ---- | --------- |
| 400  | 이메일 형식이 올바르지 않거나, provider에서 허용하지 않는 `fromAddress.email`을 지정한 경우 |
| 401  | 연동 토큰이 유효하지 않은 경우 |
| 404  | 발송 계정 연동 정보, 워크스페이스, 마케팅 이메일 도메인, 사용자 이메일 정보가 없는 경우 |
| 429  | Gmail API 한도 또는 Gmail 일시 발송 거부로 재시도가 필요한 경우 |

## 이메일 정보 조회

`GET` `/v2/email/<emailId>`

단일 이메일 정보를 조회합니다.

### Headers

| Name          | Value              |
| ------------- | ------------------ |
| Content-Type  | `application/json` |
| Authorization | `Bearer <token>`   |

### Path parameters

| Name      | Type   | Description  |
| --------- | ------ | ------------ |
| `emailId` | string | 조회하려는 메일의 id |

### Response

#### 200

```json
{
  "success": true,
  "data": {
    "email": {
      "id": "<emailId>",
      "subject": "이메일 제목",
      "from": "보낸이 주소",
      "to": ["받는이 주소"],
      "cc": ["참조 주소"],
      "bcc": ["숨은 참조 주소"],
      "status": "delivery",
      "messageId": "이메일 메시지 ID",
      "date": "2024-04-03T05:59:23.217Z"
    }
  }
}
```

| Name        | Type   | Description |
| ----------- | ------ | ----------- |
| `id`        | string | 이메일 ID |
| `subject`   | string | 이메일 제목 |
| `from`      | string | 보낸이 주소 |
| `to`        | array  | 받는이 주소 목록 |
| `cc`        | array  | 참조 주소 목록 |
| `bcc`       | array  | 숨은 참조 주소 목록 |
| `status`    | string | 발송 상태. 정상 발송은 `delivery`, 반송은 `bounced`입니다. |
| `messageId` | string | 이메일 Message-ID |
| `date`      | string | 이메일 일시 |
