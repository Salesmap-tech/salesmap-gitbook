# 회사 생성

<mark style="color:yellow;">`POST`</mark> `/v2/organization`

고객을 생성합니다.

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
//성공시
{
    "success": true,
    "data": {
        "organization":
            {
                "id": "<organizationId>",
                "name": "생성한 회사의 이름",
                "createdAt": "2024-04-08T05:25:26.020Z"
            }
}

//중복시(회사 이름 중복)
{
    "success": false,
    "message": "Bad Request",
    "reason": "중복되는 이름을 가진 기업이 존재합니다.",
    "data": {
      "id": "<organizationId>",
      "name": "생성 시도한 회사의 이름"
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

{% tab title="" %}

{% endtab %}
{% endtabs %}
