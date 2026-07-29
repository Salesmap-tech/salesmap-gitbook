# 녹음 메타 조회

<mark style="color:green;">`GET`</mark> `/v2/recording/{recordingId}`

완료된 녹음의 메타 정보를 조회합니다. 녹음이 처리 중이거나 존재하지 않으면 404를 반환합니다. `duration`의 단위는 초입니다.

**Headers**

| Name          | Value              |
| ------------- | ------------------ |
| Content-Type  | `application/json` |
| Authorization | `Bearer <token>`   |

**Path parameters**

| Name          | Type   | Description |
| ------------- | ------ | ----------- |
| `recordingId` | string | 조회하려는 녹음의 id |

**Response**

{% tabs %}
{% tab title="200" %}
```json
{
    "success": true,
    "data": {
        "recording": {
            "id": "<recordingId>",
            "title": "녹음 제목",
            "duration": 360,
            "source": "upload",
            "coreSummary": "핵심 요약",
            "createdAt": "2026-07-29T08:42:47.000Z",
            "owner": {
                "id": "<userId>",
                "name": "담당자 이름"
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
