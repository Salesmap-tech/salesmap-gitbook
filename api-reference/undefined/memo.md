# 노트 목록 조회

<mark style="color:green;">`GET`</mark> `/v2/memo`

노트 목록을 조회합니다.

**Headers**

| Name          | Value              |
| ------------- | ------------------ |
| Content-Type  | `application/json` |
| Authorization | `Bearer <token>`   |

**Query parameters**

| Name     | Type   | Description  |
| -------- | ------ | ------------ |
| `cursor` | string | 페이지네션을 위한 커서 |

**Response**

{% tabs %}
{% tab title="200" %}
```json
{
    "success": true,
    "data": {
        "memoList": [
            {
                "id": "<memoId>",
                "text": "메모 내용",
                "dealId": "<dealId>",
                "leadId": "<leadId>",
                "peopleId": "<peopleId>",
                "organizationId": "<organizationId>",
                "productId": "<productId>",
                "quoteId": "<quoteId>",
                "todoId": "<todoId>",
                "parentId": "<parentId>",
                "ownerId": "<userId>",
                "updatedAt": "2024-04-03T05:59:23.217Z",
                "createdAt": "2024-04-03T05:59:23.217Z"
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
