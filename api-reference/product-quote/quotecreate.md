# 견적서 생성

&#x20;<mark style="color:yellow;">`POST`</mark>  `/v2/quote`

특정 딜의 견적서를 생생합니다.

**Headers**

| Name          | Value              |
| ------------- | ------------------ |
| Content-Type  | `application/json` |
| Authorization | `Bearer <token>`   |

**Body parameters**

<table><thead><tr><th width="360">Name</th><th width="98">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>name</code></td><td>string</td><td><p>생성할 견적서의 이름</p><p><mark style="color:red;"><strong>Required</strong></mark></p></td></tr><tr><td><code>dealId</code></td><td>string</td><td>생성할 견적서의 딜 Id</td></tr><tr><td><code>leadId</code></td><td>string</td><td>생성할 견적서의 리드 Id</td></tr><tr><td><code>memo</code></td><td>string</td><td>견적서 생성 시 작성할 메모</td></tr><tr><td><code>fieldList</code></td><td>array</td><td>견적서의 데이터 필드</td></tr><tr><td><code>isMainQuote</code></td><td>boolean</td><td>메인 견적으로 설정할 지 여부 </td></tr><tr><td><code>quoteProductList</code></td><td>array</td><td>견적서의 상품 목록</td></tr><tr><td><code>quoteProductList[].name</code></td><td>string</td><td>견적서 상품의 이름 <br><mark style="color:red;"><strong>Required</strong></mark></td></tr><tr><td><code>quoteProductList[].productId</code></td><td>string</td><td>견적서 상품의 id<br><mark style="color:red;"><strong>Required</strong></mark> (quoteProduct가 있다면)</td></tr><tr><td><code>quoteProductList[].price</code></td><td>number</td><td>견적서 상품의 가격<br><mark style="color:red;"><strong>Required</strong></mark> (quoteProduct가 있다면)</td></tr><tr><td><code>quoteProductList[].amount</code></td><td>number</td><td>견적서 상품의 수량<br><mark style="color:red;"><strong>Required</strong></mark> (quoteProduct가 있다면)</td></tr><tr><td><code>quoteProductList[].paymentCount</code></td><td>number</td><td>견적서 상품의 결제 횟수<br><mark style="color:red;"><strong>Required</strong></mark> (단, 견적서 구성상품의 유형이 구독 상품인 경우에 한함)</td></tr><tr><td><code>quoteProductList[].paymentStartAt</code></td><td>date</td><td>견적서 상품의 시작 결제일<br><mark style="color:red;"><strong>Required</strong></mark> (단, 견적서 구성상품의 유형이 구독 상품인 경우에 한함)</td></tr><tr><td><code>quoteProductList[].fieldList</code></td><td>array</td><td>견적서 상품의 데이터 필드</td></tr></tbody></table>

{% hint style="warning" %}
2025년 4월 23일부터 quoteProduct대신 quoteProductList를 지원합니다. 이전에는 견적서 생성 시 하나의 상품만 입력할 수 있었는데, 이제 여러 상품을 입력할 수 있습니다.\
\
다만, 기존 사용자들을 위해 2025년 11월 1일까지는 quoteProduct도 동시에 지원할 예정입니다. quoteProductList 대신 quoteProduct를 body에 입력해도 정상적으로 견적서가 생성됩니다.
{% endhint %}

**Response**

{% tabs %}
{% tab title="200" %}
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
