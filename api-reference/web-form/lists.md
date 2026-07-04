# 웹폼 목록 조회

<mark style="color:green;">`GET`</mark> `/v2/webForm`

웹폼의 목록을 조회합니다.

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
        "webFormList": [
                {
                        "id": "<webFormId>",
                        "name": "웹폼 이름",
                        "description": "웹폼 설명",
                        "status": "active",
                        "folderName": "폴더 이름",
                        "viewCount": 1,
                        "submitCount": 1,
                        "createdAt": "2024-02-01T05:12:16.797Z",
                        "updatedAt": "2024-02-01T05:12:26.667Z"
                },
                {...},
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
