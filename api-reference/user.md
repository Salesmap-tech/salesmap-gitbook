# 유저 목록 조회

<mark style="color:green;">`GET`</mark> `/v2/user`

유저 목록을 조회합니다.

**Headers**

| Name          | Value              |
| ------------- | ------------------ |
| Content-Type  | `application/json` |
| Authorization | `Bearer <token>`   |

**Response**

{% tabs %}
{% tab title="200" %}
```json
{
    "success": true,
    "data": {
        "userList": [
            {
                "id": "<userId>",
                "name": "유저 이름",
                "status": "<유저 상태>",
                "email": "usermail@address.com",
                "role": "<역할 이름>",
                "updatedAt": "2024-04-03T05:59:23.217Z",
                "createdAt": "2024-04-03T05:59:23.217Z"
            },
        ]
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
