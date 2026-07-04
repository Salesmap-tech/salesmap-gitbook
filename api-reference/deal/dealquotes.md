# 딜 견적서 조회

<mark style="color:green;">`GET`</mark> `/v2/deal/<dealId>/quote`

특정 딜에 해당하는 견적서와 구성 상품들을 조회합니다.

**Headers**

| Name          | Value              |
| ------------- | ------------------ |
| Content-Type  | `application/json` |
| Authorization | `Bearer <token>`   |

**Path parameters**

| Name     | Type   | Description     |
| -------- | ------ | --------------- |
| `dealId` | string | 조회하려는 견적서의 딜 id |

**Response**

{% tabs %}
{% tab title="200" %}
```json
{
    "success": true,
    "data": {
        "quoteList": [
            {
                "id": "<quoteId>",
                "메인 견적서 여부": true,
                "공유 링크": null,
                "이름": "견적서 이름",
                "견적 구성 상품": [
                    {
                        "id": "<quoteProductId>",
                        "productId": "<productId>",
                        "금액": 10000,
                        "수량": 10,
                        "결제 횟수": 1, 
                        "시작 결제일": "2024-04-08T05:25:26.020Z",
                        "마지막 결제일": "2024-04-08T05:25:26.020Z",
                        "전체금액": 200000,
                        //이하 워스크페이스 '상품 변형' 데이터 필드
                    },
                ],
                "금액": 100000,
                "최근 작성된 노트": "최근 작성된 노트의 본문 내용",
                "최근 노트 작성일": "2024-04-08T05:25:26.020Z",
                "최근 노트 작성자": {
                    "id": "<userId>",
                    "name": "유저 이름"
                },
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
                //이하 워크스페이스 '견적서' 데이터 필드
            },
        ]
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
