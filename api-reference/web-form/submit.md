# 웹폼 제출 내역조회

<mark style="color:green;">`GET`</mark> `/v2/webForm/<webFormId>/submit`

`webFormId`에 해당하는 웹폼에 제출 된 내역들을 조회합니다.

**Headers**

| Name          | Value              |
| ------------- | ------------------ |
| Content-Type  | `application/json` |
| Authorization | `Bearer <token>`   |

**Path parameters**

| Name        | Type   | Description  |
| ----------- | ------ | ------------ |
| `webFormId` | string | 조회하려는 웹폼의 id |

**Query parameters**

| Name     | Type   | Description  |
| -------- | ------ | ------------ |
| `cursor` | string | 페이지네션을 위한 커서 |

**Response**

{% tabs %}
{% tab title="200" %}
````json
{
   {
    "success": true,
    "data": {
        "webFormSubmitList": [
            {
                "peopleId": "<peopleId>",
                "organizationId": "<organizationId>",
                "dealId": "<dealId>",
                "leadId": "<leadId>",
                "contents": [
                    {
                        "label": "이름",
                        "value": "이름 라벨에 제출 된 이름"
                    },
                    {
                        "label": "선택 필드",
                        "value": "선택지 1",
                        "childFieldList": [
                            {
                                "label": "선택필드의 종속필드 1",
                                "value": "종속 필드에 작성된 내용 "
                            },
                            {
                                "label": "선택필드의 종속필드 2",
                                "value": null
                            }
                        ]
                    },
                    {
                        "label": "전화",
                        "value": "12312341234"
                    },
                    {}
                ],
                "createdAt": "2024-04-22T02:00:11.624Z"
            },
```
        ],
        "nextCursor": "cursor",
    }
}
````
{% endtab %}

{% tab title="400" %}
```json
{
  "error": "Invalid request"
}
```
{% endtab %}
{% endtabs %}
