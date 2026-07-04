# 회사 수정

<mark style="color:yellow;">`POST`</mark> `/v2/organization/<organizationId>`

고객을 수정합니다.

**Headers**

| Name          | Value              |
| ------------- | ------------------ |
| Content-Type  | `application/json` |
| Authorization | `Bearer <token>`   |

&#x20;**Path parameters**

| Name             | Type   | Description |
| ---------------- | ------ | ----------- |
| `organizationId` | string | 수정 할 회사의 Id |

**Body parameters**

<table><thead><tr><th width="235">Name</th><th width="98">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>name</code></td><td>string</td><td>수정할 회사의 이름</td></tr><tr><td><code>memo</code></td><td>string</td><td>회사 수정 시 작성할 메모</td></tr><tr><td><code>fieldList</code></td><td>array</td><td>수정할 회사의 데이터필드</td></tr></tbody></table>

**Response**

{% tabs %}
{% tab title="201" %}
```json
{
    "success": true,
    "data": {
        "organization":
            {
                "id": "<organizationId>",
                "name": "수정한 회사의 이름",
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
