# 상품 목록 조회

<mark style="color:green;">`GET`</mark> `/v2/product`

상품의 목록을 조회합니다.

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
        "productList": [
            {
                "id": "<productId>",
                "이름": "상품 이름",
                "코드": "상품 코드",
                "유형": "일반",
                "금액": 120000,
                "단위": "상품 단위",
                "최근 작성된 노트": "최근 작성된 노트 본문",
                "최근 노트 작성일": "2024-04-08T05:25:26.020Z",
                "최근 노트 작성자": {
                    "id": "<userId>",
                    "name": "유저 이름"
                },
                "담당자": {
                    "id": "<userId>",
                    "name": "유저 이름"
                },
                "생성 날짜": "2023-11-08T06:38:32.540Z",
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
                "수정 날짜": "2024-04-08T05:25:26.020Z",
                // 이하 워크스페이스 상품 데이터 필드들
            }
        ],
        "nextCursor": "cursor",
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
