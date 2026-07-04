# 리드 히스토리 목록 조회

<mark style="color:green;">`GET`</mark> `/v2/lead/history`

리드의 히스토리 목록을 조회합니다.

**Headers**

| Name          | Value              |
| ------------- | ------------------ |
| Content-Type  | `application/json` |
| Authorization | `Bearer <token>`   |

**Query parameters**

| Name     | Type   | Description        |
| -------- | ------ | ------------------ |
| `cursor` | string | 페이지네션을 위한 커서       |
| `leadId` | string | 히스토리를 조회하려는 리드의 id |

**Response**

{% tabs %}
{% tab title="200" %}
```json
{
    "success": true,
    "data": {
        "leadHistoryList": [
            {
                "id": "<historyId>",
                "leadId":"<leadId>",
                "type": "<type>",
                "people": null,
                "organization": null,
                "fieldName": "필드 이름",
                "fieldValue": "필드 값",
                "ownerId": "<ownerId>",
                "createdAt": "2024-03-29T11:16:26.207Z"
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
