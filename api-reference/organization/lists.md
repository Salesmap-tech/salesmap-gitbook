# 회사 목록 조회

<mark style="color:green;">`GET`</mark> `/v2/organization`

회사의 목록을 조회합니다.

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
        "organizationList": [
            {
                "id": "<organizationId>",
                "이름": "회사 이름",
                "이메일": "example@email.net​",
                "전화": "01000000000",
                "프로필 사진": "회사 프로필 사진 url",
                "링크드인": "회사 링크드인 url",
                "리드 개수": 0,
                "딜 개수": 0,
                "진행중 딜 개수": 0,
                "성사된 딜 개수": 0,
                "실패된 딜 개수": 0,
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
                "제출된 웹폼 목록": [
                    {
                        "id": "<webFormId>",
                        "name": "웹폼 이름"
                    },
                    {
                        "id": "<webFormId>",
                        "name": "웹폼 이름"
                    },
                ],
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
