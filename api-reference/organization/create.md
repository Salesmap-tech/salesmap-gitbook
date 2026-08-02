# 회사 생성

<mark style="color:yellow;">`POST`</mark> `/v2/organization`

회사를 생성합니다.

**Headers**

| Name          | Value              |
| ------------- | ------------------ |
| Content-Type  | `application/json` |
| Authorization | `Bearer <token>`   |

**Body parameters**

<table><thead><tr><th width="212">Name</th><th width="98">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>name</code></td><td>string</td><td>생성하려는 회사의 이름<br><mark style="color:red;"><strong>Required</strong></mark><br>(*중복을 허용하지 않습니다. 기존에 같은 이름을 가진 회사가 존재한다면 생성 실패 메시지를 받으실 수 있습니다.)</td></tr><tr><td><code>memo</code></td><td>string</td><td>회사 생성 시 작성할 메모</td></tr><tr><td><code>fieldList</code></td><td>array</td><td>생성할 회사의 데이터필드</td></tr></tbody></table>

**Response**

{% tabs %}
{% tab title="201" %}
```json
{
  "success": true,
  "data": {
    "organization": {
      "id": "<organizationId>",
      "name": "생성한 회사의 이름",
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
  "reason": "이미 존재하는 이름입니다",
  "data": {
    "id": "<organizationId>",
    "name": "기존 회사의 이름"
  }
}
```
{% endtab %}
{% endtabs %}
