# 이메일 정보 조회

<mark style="color:green;">`GET`</mark> `/v2/email/<emailId>`

단일 이메일 정보를 조회합니다.

**Headers**

| Name          | Value              |
| ------------- | ------------------ |
| Content-Type  | `application/json` |
| Authorization | `Bearer <token>`   |

**Path parameters**

| Name      | Type   | Description  |
| --------- | ------ | ------------ |
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
                "from": "보낸이 주소",
                "to": ["받는이 주소"],
                "cc": ["참조 주소"],
                "bcc": ["숨은 참조 주소"],
                "status": "delivery", // 성장적으로 발송되면 delivery, 반송되면 bounced
                "messageId": "이메일 메시지 ID",
                "data": "2024-04-03T05:59:23.217Z"
            }
    }
}
```
{% endtab %}
{% endtabs %}
