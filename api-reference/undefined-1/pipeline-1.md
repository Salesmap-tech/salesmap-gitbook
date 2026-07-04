# 리드 파이프라인 목록 조회

<mark style="color:green;">`GET`</mark> `/v2/lead/pipeline`

리드 파이프라인과 스테이지의 목록을 조회합니다.

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
        "pipelineList": [
            {
                "id": "<pipelineId>",
                "name": "파이프라인 이름",
                "pipelineStageList": [
                    {
                        "id": "<pipelineStageId>",
                        "name": "파이프라인 스테이지 이름 1",
                        "index": 1,
                        "description": "파이프라인 스테이지1의 설명"
                    }, 
                    {
                        "id": "<pipelineStageId>",
                        "name": "파이프라인 스테이지 이름 2",
                        "index": 2,
                        "description": "파이프라인 스테이지2의 설명"
                    },
                    ,...  
                  ]
            },
            ,...
            ]
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
