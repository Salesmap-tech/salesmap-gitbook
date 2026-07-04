# TODO 목록 조회

<mark style="color:green;">`GET`</mark> `/v2/todo`

TODO의 목록을 조회합니다.

**Headers**

| Name          | Value              |
| ------------- | ------------------ |
| Content-Type  | `application/json` |
| Authorization | `Bearer <token>`   |

**Query parameters**

| Name     | Type   | Description  |
| -------- | ------ | ------------ |
| `cursor` | string | 페이지네션을 위한 커서 |

**Response**

{% tabs %}
{% tab title="200" %}
```json
{
    "success": true,
    "data": {
        "todoList": [
            {
                "id": "<todoId>",
                "dealId": "<dealId>",
                "leadId": "<leadId>",
                "peopleId": "<peopleId>",
                "organizationId": "<organizationId>",
                "내용": "Todo 내용",
                "유형": "<Todo 유형>",
                "시작 날짜": "2024-04-05T07:30:00.000Z",
                "마지막 날짜": "2024-04-05T07:45:00.000Z",
                "완료": false,
                "완료 날짜": null,
                "담당자": {
                    "id": "<userId>",
                    "name": "담당자 이름",
                },
                "팀": [
                    {"id": "<teamId>", "name":"팀 이름1"},
                    {"id": "<teamId>", "name":"팀 이름2"}, 
                    ...
                ]
                "생성 날짜": "2024-04-05T07:21:54.368Z",
                "수정 날짜": "2024-04-05T07:21:54.368Z",
                 // 이하 워크스페이스에서 추가한 데이터 필드들
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
