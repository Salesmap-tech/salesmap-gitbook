# 고객 생성

<mark style="color:yellow;">`POST`</mark> `/v2/people`

고객을 생성합니다.

**Headers**

| Name          | Value              |
| ------------- | ------------------ |
| Content-Type  | `application/json` |
| Authorization | `Bearer <token>`   |

**Body parameters**

<table><thead><tr><th width="212">Name</th><th width="98">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>name</code></td><td>string</td><td>생성하려는 고객의 이름<br><mark style="color:red;"><strong>Required</strong></mark></td></tr><tr><td><code>organizationId</code></td><td>string</td><td>고객와 연결된 회사의 Id</td></tr><tr><td><code>memo</code></td><td>string</td><td>고객 생성 시 작성할 메모</td></tr><tr><td><code>fieldList</code></td><td>array</td><td>생성할 고객의 데이터필드</td></tr></tbody></table>

**Response**

{% tabs %}
{% tab title="201" %}
```json
{
  "success": true,
  "data": {
    "people": {
      "id": "<peopleId>",
      "name": "생성한 고객의 이름",
      "createdAt": "2024-04-08T05:25:26.020Z"
    }
  }
}
```
{% endtab %}

{% tab title="400" %}
```json
{
  "success": false,
  "message": "Bad Request",
  "reason": "이미 존재하는 이메일입니다",
  "data": {
    "id": "<peopleId>",
    "name": "기존 고객의 이름"
  }
}
```
{% endtab %}
{% endtabs %}
