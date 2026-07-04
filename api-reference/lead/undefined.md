# 리드 액티비티 목록 조회

<mark style="color:green;">`GET`</mark> `/v2/lead/activity`

리드 액티비티 목록을 조회합니다.

**Headers**

| Name          | Value              |
| ------------- | ------------------ |
| Content-Type  | `application/json` |
| Authorization | `Bearer <token>`   |

**Query parameters**

| Name     | Type   | Description        |
| -------- | ------ | ------------------ |
| `cursor` | string | 페이지네션을 위한 커서       |
| `leadId` | string | 액티비티를 조회하려는 리드의 id |

**Response**

{% tabs %}
{% tab title="200" %}
```json
{
    "success": true,
    "data": {
        "leadActivityList": [
            {
                "id": "<leadActivityId>",
                "type": "<type>",
                "date": "2024-03-29T11:16:26.207Z",
                "leadId": "<dealId> or <leadId>",
                "webFormId": "<webFormId>",
                "smsId": "<smsId>",
                "todoId": "<todoId>",
                "memoId": "<memoId>",
                "emailId": "<emailId>",
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
