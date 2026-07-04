# 회사 단일 조회

<mark style="color:green;">`GET`</mark> `/v2/organization/<organizationId>`

organizationId에 해당하는 회사를 조회합니다.

**Headers**

| Name          | Value              |
| ------------- | ------------------ |
| Content-Type  | `application/json` |
| Authorization | `Bearer <token>`   |

**Path parameters**

| Name             | Type   | Description  |
| ---------------- | ------ | ------------ |
| `organizationId` | string | 조회하려는 회사의 id |

**Response**

{% tabs %}
{% tab title="200" %}
```json
{
   {
    "success": true,
    "data": {
        "organization": [
            {
                "id": "<organizationId>",
                "이름": "회사 이름",
                "이메일": "mail@mail.mail",
                "전화": "01022221111",
                "포지션": "영업 담당자",
                "프로필 사진": null,
                "링크드인": null,
                "리드 개수": 1,
                "딜 개수": 2,
                "진행중 딜 개수": 2,
                "성사된 딜 개수": 0,
                "실패된 딜 개수": 0,
                "최근 작성된 노트": "노트 내용",
                "최근 노트 작성일": "2024-03-28T07:38:47.225Z",
                "최근 노트 작성자": {
                    "id": "<userId>",
                    "name": "노트 작성 유저 이름"
                },
                "최근 제출된 웹폼": null,
                "최근 웹폼 제출 날짜": null,
                "최근 등록한 시퀀스": null,
                "최근 시퀀스 등록일": null,
                "누적 시퀀스 등록수": 0,
                "현재 진행중인 시퀀스 여부": false,
                "수신 거부 여부": false,
                "수신 거부 사유": null,
                "담당자": {
                    "id": "<userId>",
                    "name": "담당자 이름"
                },
                "생성 날짜": "2024-03-28T07:28:31.218Z",
                "팀": [
                    {
                        "id": "<teamId>",
                        "name": "팀 이름"
                    }
                ],
                "수정 날짜": "2024-03-28T07:38:47.217Z",
                "다음 TODO": "없음",
                "전체 TODO": 0,
                "완료 TODO": 0,
                "미완료 TODO": 0,
                "제출된 웹폼 목록": null,
                "등록된 시퀀스 목록": null,
                "메일 종류": null
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
