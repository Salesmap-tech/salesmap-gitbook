# 딜 생성

<mark style="color:yellow;">`POST`</mark> `/v2/deal`

딜을 생성합니다.

**Headers**

| Name          | Value              |
| ------------- | ------------------ |
| Content-Type  | `application/json` |
| Authorization | `Bearer <token>`   |

**Body parameters**

<table><thead><tr><th width="212">Name</th><th width="98">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>name</code></td><td>string</td><td>생성하려는 딜의 이름<br><mark style="color:red;"><strong>Required</strong></mark></td></tr><tr><td><code>peopleId</code></td><td>string</td><td>딜과 연결된 고객의 Id<br><mark style="color:red;"><strong>Required</strong></mark> (peopleId 혹은 organizationId 중 하나 이상은 필수)</td></tr><tr><td><code>organizationId</code></td><td>string</td><td><p>딜과 연결된 회사의 Id</p><p><mark style="color:red;"><strong>Required</strong></mark> (peopleId 혹은 organizationId 중 하나 이상은 필수)</p></td></tr><tr><td><code>status</code></td><td>string</td><td><p>딜의 상태</p><p>("Won", "Lost", "In progress" 중 하나만 가능)<br><mark style="color:red;"><strong>Required</strong></mark> </p></td></tr><tr><td><code>price</code></td><td>number</td><td>딜의 금액</td></tr><tr><td><code>memo</code></td><td>string</td><td>딜 생성 시 작성할 메모</td></tr><tr><td><code>pipelineId</code></td><td>string</td><td>딜이 소속 될 pipeline의 Id <br><mark style="color:red;"><strong>Required</strong></mark></td></tr><tr><td><code>pipelineStageId</code></td><td>string</td><td>딜이 소속 된 pipeline의 StageId<br>(pipelineId의 파이프라인에 소속된 stage만 지정가능)<br><mark style="color:red;"><strong>Required</strong></mark></td></tr><tr><td><code>fieldList</code></td><td>array</td><td>생성할 딜의 데이터필드</td></tr></tbody></table>

**Request**

{% tabs %}
{% tab title="Example" %}
```json
{
  "name": "딜 명",
  "organizationId": "<회사 ID>",
  "peopleId": "<고객 ID>",
  "pipelineId": "<파이프라인 ID>",
  "pipelineStageId": "<파이프라인 단계 ID>",
  "status": "In progress",
  "fieldList": [
    {
      "name" : "<필드 이름>",
      "stringValue": "<텍스트 입력>"
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
        "deal":
            {
                "id": "<dealId>",
                "name": "생성한 딜의 이름",
                "createdAt": "2024-04-08T05:25:26.020Z"
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
