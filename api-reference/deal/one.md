# 딜 단일 조회

<mark style="color:green;">`GET`</mark> `/v2/deal/<dealId>`

dealId에 해당하는 딜을 조회합니다. 응답의 `data.deal`은 배열이며 첫 항목에서 값을 읽습니다. 필드 값은 현재 워크스페이스의 필드명을 키로 반환하고, 값이 없으면 `null`입니다. 담당자 필드는 `{id, name}` 또는 `null`이며 `ownerId`, `ownerName`, `customFieldList` 형식으로 반환하지 않습니다. 필드명을 변경하면 연동 코드의 필드명도 함께 변경해야 합니다.

**Headers**

| Name          | Value              |
| ------------- | ------------------ |
| Content-Type  | `application/json` |
| Authorization | `Bearer <token>`   |

**Path parameters**

| Name     | Type   | Description |
| -------- | ------ | ----------- |
| `dealId` | string | 조회하려는 딜의 id |

**Response**

{% tabs %}
{% tab title="200" %}
```json
{
    "success": true,
    "data": {
        "deal": [
            {
                "id": "<dealId>",
                "peopleId": "<peopleId>",
                "organizationId": "<organizationId>",
                "이름": "딜 이름",
                "파이프라인": {
                    "id": "<pipelineId>",
                    "name": "기본 파이프라인"
                },
                "금액": null,
                "상태": "SQL",
                "마감일": null,
                "수주 예정일": null,
                "최근 이메일 오픈일": null,
                "소스": "데이터 업로드",
                "최근 작성된 노트": null,
                "최근 노트 작성일": null,
                "최근 노트 작성자": null,
                "최근 제출된 웹폼": null,
                "최근 웹폼 제출 날짜": null,
                "상담 일수": 0,
                "정체 일수": 0,
                "파이프라인 단계": {
                    "id": "<pipelineStageId>",
                    "name": "최종 교섭과 의사 기본"
                },
                "최근 등록한 시퀀스": null,
                "최근 시퀀스 등록일": null,
                "누적 시퀀스 등록수": 0,
                "현재 진행중인 시퀀스 여부": false,
                "담당자": {
                    "id": "<userId>",
                    "name": "담당자 이름"
                },
                "생성 날짜": "2024-03-26T07:08:22.820Z",
                "팀": [
                    {
                        "id": "7653ce41-f8d2-43a6-abb3-d80f3517a2fe",
                        "name": "세일즈맵 파워팀"
                    },
                    {
                        "id": "adc965d5-5810-4313-b287-254faab7bdb3",
                        "name": "와"
                    }
                ],
                "수정 날짜": "2024-04-19T05:50:40.008Z",
                "메인 견적 상품 리스트": null,
                "다음 TODO": "없음",
                "전체 TODO": 0,
                "완료 TODO": 0,
                "미완료 TODO": 0,
                "등록된 시퀀스 목록": null,
                "팔로워": null,
                "참여자": null,
            }
        ]
    }
}
```
{% endtab %}

{% tab title="400" %}
존재하지 않거나 삭제된 딜은 `400`으로 응답합니다.

```json
{
  "success": false,
  "message": "Bad Request",
  "reason": "딜을 찾을 수 없습니다."
}
```
{% endtab %}
{% endtabs %}
