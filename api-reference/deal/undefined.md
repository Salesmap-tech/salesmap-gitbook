# 딜 액티비티 목록 조회

<mark style="color:green;">`GET`</mark> `/v2/deal/activity`

딜의 액티비티 목록을 조회합니다. `types`로 활동 유형을 쉼표로 구분해 필터링할 수 있고, `startDate`와 `endDate`로 활동 발생 기간을 제한할 수 있습니다.

**Headers**

| Name          | Value              |
| ------------- | ------------------ |
| Content-Type  | `application/json` |
| Authorization | `Bearer <token>`   |

**Query parameters**

| Name        | Type   | Description |
| ----------- | ------ | ----------- |
| `cursor`    | string | 페이지네이션을 위한 커서 |
| `dealId` | string | 액티비티를 조회하려는 딜의 id |
| `types`     | string | 조회할 활동 유형 목록. 여러 값은 쉼표로 구분합니다. 예: `MemoCreate,RecordingCreate` |
| `startDate` | string | 조회 시작일. `YYYY-MM-DD` 또는 offset이 포함된 ISO date-time을 지원합니다. 날짜만 입력하면 KST 일 시작 시각으로 해석합니다. |
| `endDate`   | string | 조회 종료일. `YYYY-MM-DD` 또는 offset이 포함된 ISO date-time을 지원합니다. 날짜만 입력하면 KST 일 종료 시각으로 해석합니다. |

**Response**

{% tabs %}
{% tab title="200" %}
```json
{
    "success": true,
    "data": {
        "dealActivityList": [
            {
                "id": "<dealActivityId>",
                "type": "<type>",
                "date": "2024-03-29T11:16:26.207Z",
                "dealStatus": "<dealStatus>",
                "dealId": "<dealId>",
                "webFormId": "<webFormId>",
                "smsId": "<smsId>",
                "todoId": "<todoId>",
                "memoId": "<memoId>",
                "emailMessageId": "<emailMessageId>",
                "recordingId": "<recordingId>"
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
