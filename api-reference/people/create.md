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
<pre class="language-json"><code class="lang-json"><strong>//성공시
</strong><strong>{
</strong>    "success": true,
    "data": {
        "people":
            {
                "id": "&#x3C;peopleId>",
                "name": "생성한 고객의 이름",
                "createdAt": "2024-04-08T05:25:26.020Z"
            }
}
//중복(고객 이메일 동일)
{
    "success": false,
    "message": "Bad Request",
    "reason": "동일한 이메일을 가진 고객이 존재합니다.",
    "data": {
      "id": "&#x3C;peopleId>",
      "name": "생성시도한 고객 이름"
            }
}

</code></pre>
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
