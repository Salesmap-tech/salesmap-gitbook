# 고객 히스토리 목록 조회

<mark style="color:green;">`GET`</mark> `/v2/people/history`

고객의 히스토리 목록을 조회합니다.

**Headers**

| Name          | Value              |
| ------------- | ------------------ |
| Content-Type  | `application/json` |
| Authorization | `Bearer <token>`   |

**Query parameters**

| Name       | Type   | Description        |
| ---------- | ------ | ------------------ |
| `cursor`   | string | 페이지네션을 위한 커서       |
| `peopleId` | string | 히스토리를 조회하려는 고객의 id |

**Response**

{% tabs %}
{% tab title="200" %}
```json
{
    "success": true,
    "data": {
        "peopleHistoryList": [
            {
                "id": "<historyId>",
                "peopleId": "<peopleId>",
                "type": "<type>",
                "source": {
                    "type": "user",
                    "id": "<sourceId>",
                    "name": "홍길동"
                },
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

| Path | Type | Description |
| --- | --- | --- |
| `data.peopleHistoryList[].source` | object | 히스토리를 생성한 주체 정보입니다. |
| `data.peopleHistoryList[].source.type` | string | 생성 주체의 종류입니다. 예: `user`, `workflow`, `sequence`, `api` |
| `data.peopleHistoryList[].source.id` | string\|null | 생성 주체의 식별자입니다. |
| `data.peopleHistoryList[].source.name` | string\|null | 생성 주체의 이름 스냅샷입니다. |
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
