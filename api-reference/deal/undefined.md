# 딜 액티비티 목록 조회

<mark style="color:green;">`GET`</mark> `/v2/deal/activity`

딜 액티비티 목록을 조회합니다.

**Headers**

| Name          | Value              |
| ------------- | ------------------ |
| Content-Type  | `application/json` |
| Authorization | `Bearer <token>`   |

**Query parameters**

| Name     | Type   | Description       |
| -------- | ------ | ----------------- |
| `cursor` | string | 페이지네션을 위한 커서      |
| `dealId` | string | 액티비티를 조회하려는 딜의 id |

**Response**

{% tabs %}
{% tab title="200" %}
```json
{
    "success": true,
    "data": {
        "dealActivityList": [
            {
                "id": "<dealActivityId>",
                "type": "<type>",
                "date": "2024-03-29T11:16:26.207Z",
                "dealStatus": "<status>",
                "dealId": "<dealId> or <leadId>",
                "webFormId": "<webFormId>",
                "smsId": "<smsId>",
                "todoId": "<todoId>",
                "memoId": "<memoId>",
                "emailMessageId": "<emailMessageId>",
            }
        ],
        "nextCursor": "cursor"
    }
}
```
{% endtab %}

{% tab title="40x" %}
```json
{
    "success": false,
    "message": "에러 메세지"
}
```
{% endtab %}
{% endtabs %}
