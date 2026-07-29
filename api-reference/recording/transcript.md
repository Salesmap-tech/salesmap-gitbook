# 녹음 전사문 조회

<mark style="color:green;">`GET`</mark> `/v2/recording/{recordingId}/transcript`

완료된 녹음의 발화 구간과 화자 정보를 조회합니다. 녹음이 처리 중이거나 존재하지 않으면 404를 반환합니다. `startTime`과 `endTime`의 단위는 밀리초입니다.

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
        "recordingTranscript": {
            "transcriptSegmentList": [
                {
                    "startTime": 0,
                    "endTime": 3200,
                    "text": "안녕하세요.",
                    "speakerId": "1",
                    "confidence": 0.98
                }
            ],
            "speakerInfoList": [
                {
                    "speakerId": "1",
                    "label": "담당자"
                }
            ]
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
