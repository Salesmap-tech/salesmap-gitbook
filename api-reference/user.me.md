# 내 정보 조회

<mark style="color:green;">`GET`</mark> `/v2/user/me`

토큰을 기반으로 유저 정보를 조회합니다.

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
        "user": {
            "id": "<userId>",
            "name": "유저 이름",
            "status": "<유저 상태>",
            "updatedAt": "2024-04-03T05:59:23.217Z",
            "createdAt": "2024-04-03T05:59:23.217Z",
            "room": {
                "id": "<roomId>",
                "name": "워크스페이스 이름"
            }
        }
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
