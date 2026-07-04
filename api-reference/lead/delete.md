# 리드 삭제

<mark style="color:yellow;">`POST`</mark> `/v2/lead/<leadId>/delete`

특정 리드를 삭제합니다.

**Headers**

| Name          | Value              |
| ------------- | ------------------ |
| Content-Type  | `application/json` |
| Authorization | `Bearer <token>`   |

**Path parameters**

| Name   | Type   | Description |
| ------ | ------ | ----------- |
| leadId | string | 삭제 할 리드의 Id |

**Response**

{% tabs %}
{% tab title="200" %}
```json
{
    "success": true,
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
