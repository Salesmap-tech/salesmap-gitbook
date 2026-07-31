# 견적서 생성

&#x20;<mark style="color:yellow;">`POST`</mark>  `/v2/quote`

특정 딜 또는 리드의 견적서를 생성합니다.

**Headers**

| Name          | Value              |
| ------------- | ------------------ |
| Content-Type  | `application/json` |
| Authorization | `Bearer <token>`   |

**Body parameters**

<table><thead><tr><th width="360">Name</th><th width="98">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>name</code></td><td>string</td><td><p>생성할 견적서의 이름</p><p><mark style="color:red;"><strong>Required</strong></mark></p></td></tr><tr><td><code>dealId</code></td><td>string</td><td>생성할 견적서의 딜 Id. dealId와 leadId 중 정확히 하나 필요</td></tr><tr><td><code>leadId</code></td><td>string</td><td>생성할 견적서의 리드 Id. dealId와 leadId 중 정확히 하나 필요</td></tr><tr><td><code>memo</code></td><td>string</td><td>견적서 생성 시 작성할 메모</td></tr><tr><td><code>fieldList</code></td><td>array</td><td>견적서의 데이터 필드</td></tr><tr><td><code>isMainQuote</code></td><td>boolean</td><td>메인 견적으로 설정할 지 여부</td></tr><tr><td><code>quoteProductList</code></td><td>array</td><td>견적서의 상품 목록</td></tr><tr><td><code>quoteProductList[].name</code></td><td>string</td><td>견적서 상품의 이름<br><mark style="color:red;"><strong>Required</strong></mark></td></tr><tr><td><code>quoteProductList[].productId</code></td><td>string</td><td>견적서 상품의 id<br><mark style="color:red;"><strong>Required</strong></mark> (quoteProductList 항목마다)</td></tr><tr><td><code>quoteProductList[].price</code></td><td>number</td><td>견적서 상품의 가격. 0 이상<br><mark style="color:red;"><strong>Required</strong></mark> (quoteProductList 항목마다)</td></tr><tr><td><code>quoteProductList[].amount</code></td><td>number</td><td>견적서 상품의 수량. 0 이상<br><mark style="color:red;"><strong>Required</strong></mark> (quoteProductList 항목마다)</td></tr><tr><td><code>quoteProductList[].paymentCount</code></td><td>number</td><td>견적서 상품의 결제 횟수</td></tr><tr><td><code>quoteProductList[].paymentStartAt</code></td><td>date</td><td>견적서 상품의 시작 결제일</td></tr><tr><td><code>quoteProductList[].fieldList</code></td><td>array</td><td>견적서 상품의 데이터 필드</td></tr></tbody></table>

{% hint style="info" %}
`dealId`와 `leadId` 중 정확히 하나를 입력해야 합니다. 견적 상품을 추가할 때는 `quoteProductList`를 사용하며, 각 항목의 `name`, `productId`, `price`, `amount`는 필수입니다. 구독형 상품은 1 이상의 `paymentCount`와 `paymentStartAt`을 함께 입력해야 하며, 일반 상품에는 두 값을 입력할 수 없습니다.
{% endhint %}

**Response**

{% tabs %}
{% tab title="201" %}
```json
{
    "success": true,
    "data": {
        "quote": {
            "id": "<quoteId>",
             "name": "견적서 이름",
             "createdAt": "2024-04-16T07:18:17.516Z"
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
