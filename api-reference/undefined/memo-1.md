# 노트 단일 조회

<mark style="color:green;">`GET`</mark> `/v2/memo/<memoId>`

단일 노트를 조회합니다.

**Headers**

| Name          | Value              |
| ------------- | ------------------ |
| Content-Type  | `application/json` |
| Authorization | `Bearer <token>`   |

**Path parameters**

| Name     | Type   | Description  |
| -------- | ------ | ------------ |
| `memoId` | string | 조회하려는 메모의 id |

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
