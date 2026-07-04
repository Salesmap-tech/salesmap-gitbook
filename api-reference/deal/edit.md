# 딜 수정

<mark style="color:yellow;">`POST`</mark> `/v2/deal/<dealId>`

딜을 수정합니다.

**Headers**

| Name          | Value              |
| ------------- | ------------------ |
| Content-Type  | `application/json` |
| Authorization | `Bearer <token>`   |

&#x20;**Path parameters**

| Name     | Type   | Description |
| -------- | ------ | ----------- |
| `dealId` | string | 수정 할 딜의 Id  |

**Body parameters**

<table><thead><tr><th width="235">Name</th><th width="98">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>name</code></td><td>string</td><td>수정할 딜의 이름</td></tr><tr><td><code>peopleId</code></td><td>string</td><td>수정할 딜과 연결된 고객의 Id</td></tr><tr><td><code>organizationId</code></td><td>string</td><td>수정할 딜과 연결된 회사의 Id</td></tr><tr><td><code>status</code></td><td>string</td><td>수정할 딜의 상태</td></tr><tr><td><code>price</code></td><td>number</td><td>수정할 딜의 금액</td></tr><tr><td><code>memo</code></td><td>string</td><td>딜 수정 시 작성할 메모</td></tr><tr><td><code>pipelineId</code></td><td>string</td><td>수정할 딜이 소속 될 pipeline의 Id </td></tr><tr><td><code>pipelineStageId</code></td><td>string</td><td>수정할 딜이 소속 될 pipeline의 StageId<br>(pipelineId의 파이프라인에 소속된 stage만 지정가능)<br><mark style="color:red;"><strong>Required</strong></mark> (pipeline을 선택한 경우)</td></tr><tr><td><code>fieldList</code></td><td>array</td><td>수정할 딜의 데이터필드</td></tr></tbody></table>

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
                "name": "수정한 딜의 이름",
                "updatedAt": "2024-04-08T05:25:26.020Z"
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
