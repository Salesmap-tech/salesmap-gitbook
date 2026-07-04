# 딜 목록 조회

<mark style="color:green;">`GET`</mark> `/v2/deal`

딜의 목록을 조회합니다.

**Headers**

| Name          | Value              |
| ------------- | ------------------ |
| Content-Type  | `application/json` |
| Authorization | `Bearer <token>`   |

**Query parameters**

| Name                | Type   | Description              |
| ------------------- | ------ | ------------------------ |
| `cursor`            | string | 페이지네션을 위한 커서             |
| `pipelineName`      | string | 조회를 원하는 딜의 파이프라인 이름      |
| `pipelineStageName` | string | 조회를 원하는 딜의 파이프라인 스테이지 이름 |

**Response**

{% tabs %}
{% tab title="200" %}
```json
{
    "success": true,
    "data": {
        "dealList": [
            {
                "id": "<dealId>",
                "peopleId": "<peopleId>",
                "organizationId": "<organizationId>",
                "이름": "딜 이름",
                "파이프라인": {
                    "id": "<pipelineId>",
                    "name": "파이프라인 이름"
                },
                "파이프라인 단계": {
                    "id": "<pipelineStageId>",
                    "name": "파이프라인 단계 이름"
                },
                "메인 견적 상품 리스트": [
                    {
                        "id": "<productId>",
                        "name": "상품 이름1"
                    },
                    {
                        "id": "<productId>",
                        "name": "상품 이름2"
                    },
                ],
                "금액": 24000,
                "상태": "Convert",
                "마감일": "2024-04-08T05:25:26.020Z",
                "수주 예정일": "2024-04-08T05:25:26.020Z",
                "최근 이메일 오픈일": "2024-04-08T05:25:26.020Z",
                "소스": "데이터 업로드"
                "최근 작성된 노트": "최근 작성된 노트 본문",
                "최근 노트 작성일": "2024-04-08T05:25:26.020Z",
                "최근 노트 작성자": {
                    "id": "<userId>",
                    "name": "유저 이름"
                },
                "최근 제출된 웹폼": {
                    "id": "<webFormId>",
                    "name": "웹폼 이름"
                },
                "최근 웹폼 제출 날짜": "2024-04-08T05:25:26.020Z",
                "최근 등록한 시퀀스": {
                    "id": "<sequenceId>",
                    "name": "시퀀스 이름"
                },
                "최근 시퀀스 등록일": "2024-04-08T05:25:26.020Z",
                "누적 시퀀스 등록수": 0,
                "현재 진행중인 시퀀스 여부": false,
                "담당자": {
                    "id": "<userId>",
                    "name": "유저 이름"
                },
                "생성 날짜": "2024-04-01T06:37:57.925Z",
                "팀": [
                    {
                        "id": "7653ce41-f8d2-43a6-abb3-d80f3517a2fe",
                        "name": "세일즈맵 파워팀"
                    },
                ],
                "수정 날짜": "2024-04-08T05:10:19.676Z",
                "다음 TODO": "없음",
                "전체 TODO": 5,
                "완료 TODO": 2,
                "미완료 TODO": 3,
                "등록된 시퀀스 목록": [
                    {
                        "id": "<sequenceId>",
                        "name": "시퀀스 이름"
                    },
                    {
                        "id": "<sequenceId>",
                        "name": "시퀀스 이름"
                    },
                ],
                // 이하 워크스페이스에서 추가한 데이터 필드들
            },
        ],
        "nextCurosr": "cursor"
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
