# 회사 액티비티 목록 조회

<mark style="color:green;">`GET`</mark> `/v2/organization/activity`

딜 액티비티 목록을 조회합니다.

**Headers**

| Name          | Value              |
| ------------- | ------------------ |
| Content-Type  | `application/json` |
| Authorization | `Bearer <token>`   |

**Query parameters**

| Name             | Type   | Description        |
| ---------------- | ------ | ------------------ |
| `cursor`         | string | 페이지네션을 위한 커서       |
| `organizationId` | string | 액티비티를 조회하려는 회사의 id |

**Response**

{% tabs %}
{% tab title="200" %}
```json
{
    "success": true,
    "data": {
        "organizationActivityList": [
            {
                "id": "<organizationActivityId>",
                "type": "<type>",
                "date": "2024-03-29T11:16:26.207Z",
                "organizationId": "<organizationId>",
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
