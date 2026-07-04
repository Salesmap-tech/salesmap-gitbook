# 리드 단일 조회

<mark style="color:green;">`GET`</mark> `/v2/lead/<leadId>`

leadId에 해당하는 리드를 조회합니다.

**Headers**

| Name          | Value              |
| ------------- | ------------------ |
| Content-Type  | `application/json` |
| Authorization | `Bearer <token>`   |

**Path parameters**

| Name     | Type   | Description  |
| -------- | ------ | ------------ |
| `leadId` | string | 조회하려는 리드의 id |

**Response**

{% tabs %}
{% tab title="200" %}
```json
{
    "success": true,
    "data": {
        "lead": [
            {
                "id": "<leadId>",
                "peopleId": "<peopleId>",
                "organizationId": "<organizationId>",
                "이름": "리드 이름",
                "파이프라인": null,
                "금액": null,
                "상태": "New",
                "마감일": null,
                "수주 예정일": null,
                "최근 이메일 오픈일": null,
                "소스": "직접 생성",
                "최근 작성된 노트": null,
                "최근 노트 작성일": null,
                "최근 노트 작성자": null,
                "최근 제출된 웹폼": null,
                "최근 웹폼 제출 날짜": null,
                "상담 일수": 0,
                "정체 일수": 0,
                "파이프라인 단계": null,
                "최근 등록한 시퀀스": null,
                "최근 시퀀스 등록일": null,
                "누적 시퀀스 등록수": 0,
                "현재 진행중인 시퀀스 여부": false,
                "담당자": {
                    "id": "<userId>",
                    "name": "담당자 이름"
                },
                "생성 날짜": "2024-04-19T06:41:34.299Z",
                "팀": [
                    {
                        "id": "<teamId>",
                        "name": "팀 이름"
                    },
                    {
                        "id": "<teamId>",
                        "name": "팀 이름2"
                    }
                ],
                "수정 날짜": "2024-04-19T06:41:34.299Z",
                "메인 견적 상품 리스트": null,
                "다음 TODO": "없음",
                "전체 TODO": 0,
                "완료 TODO": 0,
                "미완료 TODO": 0,
                "등록된 시퀀스 목록": null,
            }
        ]
    }
}
```
{% endtab %}

{% tab title="400" %}
```json
{
  "error": "Invalid request"
}
```
{% endtab %}
{% endtabs %}
