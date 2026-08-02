# 견적서 생성

<mark style="color:yellow;">`POST`</mark> `/v2/quote`

딜 또는 리드에 연결된 견적서를 생성합니다. `dealId`와 `leadId` 중 정확히 하나를 입력해야 합니다.

**Headers**

| Name | Value |
| --- | --- |
| Content-Type | `application/json` |
| Authorization | `Bearer <token>` |

**Body parameters**

| Name | Type | Description |
| --- | --- | --- |
| `name` | string | 생성할 견적서의 이름. 공백이 아닌 문자열이어야 합니다.<br><mark style="color:red;"><strong>Required</strong></mark> |
| `dealId` | string | 견적서를 연결할 딜 ID. `leadId`와 동시에 입력할 수 없습니다. |
| `leadId` | string | 견적서를 연결할 리드 ID. `dealId`와 동시에 입력할 수 없습니다. |
| `memo` | string | 견적서 생성 시 함께 작성할 메모 |
| `fieldList` | array | 견적서의 데이터 필드 |
| `isMainQuote` | boolean | 메인 견적으로 설정할지 여부 |
| `quoteProductList` | array | 견적서의 상품 목록 |
| `quoteProductList[].name` | string | 견적서 상품의 이름<br><mark style="color:red;"><strong>Required</strong></mark> |
| `quoteProductList[].productId` | string | 견적서 상품의 ID<br><mark style="color:red;"><strong>Required</strong></mark> |
| `quoteProductList[].price` | number | 견적서 상품의 가격. 0 이상이어야 합니다.<br><mark style="color:red;"><strong>Required</strong></mark> |
| `quoteProductList[].amount` | number | 견적서 상품의 수량. 0 이상이어야 합니다.<br><mark style="color:red;"><strong>Required</strong></mark> |
| `quoteProductList[].paymentCount` | number | 결제 횟수. 구독형 상품에서는 `paymentStartAt`과 함께 필요하며 일반 상품에서는 사용하지 않습니다. |
| `quoteProductList[].paymentStartAt` | string (date-time) | 시작 결제일. 구독형 상품에서는 `paymentCount`와 함께 필요하며 일반 상품에서는 사용하지 않습니다. |
| `quoteProductList[].fieldList` | array | 견적서 상품의 데이터 필드 |

{% hint style="info" %}
결제 정보는 상품 유형에 따라 서버에서 검증합니다. 구독형 상품에는 `paymentCount`와 `paymentStartAt`이 모두 필요하고, 일반 상품에는 입력하지 않습니다.
{% endhint %}

**Request**

{% tabs %}
{% tab title="Deal quote" %}
```json
{
  "name": "견적서 이름",
  "dealId": "<dealId>",
  "isMainQuote": true,
  "quoteProductList": [
    {
      "name": "상품 이름",
      "productId": "<productId>",
      "price": 10000,
      "amount": 1
    }
  ]
}
```
{% endtab %}

{% tab title="Subscription product" %}
```json
{
  "name": "구독 견적서",
  "leadId": "<leadId>",
  "quoteProductList": [
    {
      "name": "구독 상품",
      "productId": "<productId>",
      "price": 10000,
      "amount": 1,
      "paymentCount": 12,
      "paymentStartAt": "2026-08-02T00:00:00.000Z"
    }
  ]
}
```
{% endtab %}
{% endtabs %}

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
