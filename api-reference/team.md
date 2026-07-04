# 팀 목록 조회

<mark style="color:green;">`GET`</mark> `/v2/team`

팀 목록을 조회합니다.

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
        "teamList": [
            {
                "id": "<teamId>",
                "name": "팀 이름",
                "description": "팀 설명",
                "teammateList": [
                    {
                        "id": "<userId>",
                        "name": "유저 이름1"
                    },
                    {
                        "id": "<userId>",
                        "name": "유저 이름2"
                    },
                ]
            }
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
