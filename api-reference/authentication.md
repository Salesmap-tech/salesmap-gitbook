---
description: “세일즈맵 API 인증을 위해 토큰을 발급받으세요👆”
---

# Authentication

{% hint style="info" %}
토큰을 이용하여 세일즈맵 API를 호출하면 토큰을 생성한 유저의 워크스페이스에 생성되며, 담당자는 토큰을 생성한 유저로 설정됩니다.
{% endhint %}

#### ​[​](https://forward-amaranth-cod.mintlify.app/developer/authentication)🔒 토큰 생성하기 <a href="#undefined" id="undefined"></a>

* ‘개인 설정 / 연동 ’ 메뉴로 이동 후 API 연동 버튼을 눌러주세요.
* API 연동 화면에서 새 토큰 생성 버튼을 클릭해주세요.
* 세일즈맵의 데이터에 액세스하는 데 사용될 수 있으므로 API 토큰을 안전하게 유지해주세요.

{% hint style="info" %}
토큰은 여러번 생성 할 수 있으며, 토큰을 생성하면 기존의 토큰은 만료됩니다.
{% endhint %}

### CRM REST API v2의 호출 IP 제한

워크스페이스에 허용 IP 목록이 설정되어 있으면, 기본 관리자 역할이 아닌 사용자의 API 토큰으로 보내는 요청은 등록된 IP에서 호출해야 합니다. 호출 IP를 확인할 수 없거나 목록에 없는 IP이면 `403 Forbidden`을 반환합니다.

기본 관리자 역할 사용자의 토큰에는 이 IP 제한이 적용되지 않습니다. 토큰 인증과 엔드포인트별 권한 검사는 여전히 적용됩니다.
