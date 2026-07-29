# 이메일 정보 조회

<mark style="color:green;">`GET`</mark> `/v2/email/{emailId}`

단일 이메일 정보를 조회합니다. 재조회 한도 복구 중인 내부 placeholder Message-ID는 외부 threading 입력으로 사용되지 않도록 빈 문자열로 반환됩니다.

**Headers**

| Name          | Value              |
| ------------- | ------------------ |
| Content-Type  | `application/json` |
| Authorization | `Bearer <token>`   |

**Path parameters**

| Name      | Type   | Description |
| --------- | ------ | ----------- |
| `emailId` | string | 조회하려는 메일의 id |

**Response**

{% tabs %}
{% tab title="200" %}
```json
{
    "success": true,
    "data": {
        "email": {
            "id": "<emailId>",
            "subject": "이메일 제목",
            "from": "sender@example.com",
            "to": ["receiver@example.com"],
            "cc": [],
            "bcc": [],
            "status": "delivery",
            "messageId": "<messageId>",
            "date": "2024-04-03T05:59:23.217Z",
            "snippet": "본문 미리보기",
            "htmlBody": "<p>본문</p>",
            "text": "본문"
        }
    }
}
```
{% endtab %}
{% endtabs %}
