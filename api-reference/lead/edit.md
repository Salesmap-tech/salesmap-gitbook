# 리드 수정

<mark style="color:yellow;">`POST`</mark> `/v2/lead/<leadId>`

딜을 수정합니다.

**Headers**

| Name          | Value              |
| ------------- | ------------------ |
| Content-Type  | `application/json` |
| Authorization | `Bearer <token>`   |

&#x20;**Path parameters**

| Name     | Type   | Description |
| -------- | ------ | ----------- |
| `leadId` | string | 수정 할 리드의 Id |

**Body parameters**

<table><thead><tr><th width="235">Name</th><th width="98">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>name</code></td><td>string</td><td>수정할 리드의 이름</td></tr><tr><td><code>peopleId</code></td><td>string</td><td>수정할 리드과 연결된 고객의 Id</td></tr><tr><td><code>organizationId</code></td><td>string</td><td>수정할 리드과 연결된 회사의 Id</td></tr><tr><td><code>memo</code></td><td>string</td><td>리드 수정 시 작성할 메모</td></tr><tr><td><code>fieldList</code></td><td>array</td><td>수정할 리드의 데이터필드</td></tr><tr><td></td><td></td><td></td></tr><tr><td></td><td></td><td></td></tr></tbody></table>

**Response**

{% tabs %}
{% tab title="201" %}
```json
{
    "success": true,
    "data": {
        "lead":
            {
                "id": "<leadId>",
                "name": "수정한 리드의 이름",
                "updatedAt": "2024-04-08T05:25:26.020Z"
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
