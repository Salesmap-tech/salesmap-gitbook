# 상품 생성

<mark style="color:yellow;">`POST`</mark> `/v2/product`

상품을 생성합니다.

**Headers**

| Name          | Value              |
| ------------- | ------------------ |
| Content-Type  | `application/json` |
| Authorization | `Bearer <token>`   |

**Body parameters**

<table><thead><tr><th width="212">Name</th><th width="98">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>name</code></td><td>string</td><td>생성하려는 상품의 이름<br><mark style="color:red;"><strong>Required</strong></mark></td></tr><tr><td><code>price</code></td><td>number</td><td>생성할 상품의 가격<br><mark style="color:red;"><strong>Required</strong></mark></td></tr><tr><td><code>memo</code></td><td>string</td><td>상품 생성 시 작성할 메모</td></tr><tr><td><code>fieldList</code></td><td>array</td><td>생성할 상품의 데이터필드<br><sup><sub>*상품의 상태 (활성화 / 비활성화) 를 입력하지 않으면 활성화 상태로 생성됩니다.</sub></sup><br><sup><sub>*상품의 종류 (일반 / 구독 (월간) / 구독 (연간))를 입력하지 않으면 일반 상품으로 생성됩니다.</sub></sup></td></tr></tbody></table>

**Response**

{% tabs %}
{% tab title="201" %}
```json
{
    "success": true,
    "data": {
        "product":
            {
                "id": "<productId>",
                "name": "생성한 상품의 이름",
                "createdAt": "2024-04-08T05:25:26.020Z"
            }
}
```
{% endtab %}
{% endtabs %}
