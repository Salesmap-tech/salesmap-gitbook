---
description: 본 문서에서는 세일즈맵 MCP 연결 방법에 대해 다룹니다.
---

# 시작하기

### 1단계: 세일즈맵 API 토큰 준비

1. [세일즈맵](https://salesmap.kr) 접속 → 좌측 하단 **설정**
2. **개인 → 연동 → API** 메뉴로 이동
3. **이미 토큰이 있다면 → 복사** / **토큰이 없다면 → 토큰 생성** 클릭 후 복사

{% hint style="warning" %}
**토큰은 절대 다른 사람과 공유하지 마세요.**\
토큰을 재발급하면 기존 연동이 끊어질 수 있습니다. 이미 토큰이 있다면 새로 만들지 말고 복사해서 사용하세요.
{% endhint %}

***

### 2단계: AI에 연결

{% tabs %}
{% tab title="Claude" %}
{% hint style="info" %}
요건: Claude 유료 플랜 (Pro/Max/Team/Enterprise)
{% endhint %}

1. [claude.ai](https://claude.ai) / Claude Desktop 접속 → 좌측 하단 프로필 → 설정 → **커넥터**
2.  추가 → **커스텀 커넥터 추가** 클릭<br>

    <figure><img src="../.gitbook/assets/image (14).png" alt="" width="563"><figcaption></figcaption></figure>
3.  아래와 같이 입력 후 **추가**:

    * 이름: `세일즈맵`
    * 원격 MCP 서버 URL: `https://mcp.ai.salesmap.kr/mcp`
    * (고급 설정은 건드리지 않아도 됩니다)

    <figure><img src="../.gitbook/assets/image (9).png" alt="" width="375"><figcaption></figcaption></figure>
4. **연결** 클릭
5.  복사해 둔 **API 토큰을 붙여넣고 \[연결 승인]** 클릭<br>

    <figure><img src="../.gitbook/assets/image (16).png" alt="" width="413"><figcaption></figcaption></figure>
{% endtab %}

{% tab title="ChatGPT" %}
{% hint style="info" %}
요건: ChatGPT 유료 플랜 (Plus/Pro/Business/Enterprise) + 개발자 모드
{% endhint %}

1. [chatgpt.com](https://chatgpt.com) / chatGPT 앱 접속 → 프로필 → **설정**
2. 보안 및 로그인 → **개발자 모드 켜기**
3. 플러그인 → 추가
4. 커넥터 목록에서 **만들기(Create)** 클릭 후 입력:
   * 이름: `세일즈맵`
   * 연결: `https://mcp.ai.salesmap.kr/mcp`
   * 인증: **OAuth**

<figure><img src="../.gitbook/assets/image (18).png" alt="" width="345"><figcaption></figcaption></figure>

4. 만들기 클릭 → **세일즈맵 계정으로 로그인**
5. 복사해 둔 **API 토큰을 붙여넣고 \[연결 승인]** 클릭

<figure><img src="../.gitbook/assets/image (19).png" alt="" width="413"><figcaption></figcaption></figure>
{% endtab %}

{% tab title="Gemini" %}
{% hint style="warning" %}
현재 Google 정책상 한국 계정에서는 MCP 연동을 지원하지 않습니다.
{% endhint %}

1. [gemini.google.com/apps](https://gemini.google.com/apps) 접속
2. 앱 추가에 서버 URL 입력: https//mcp.ai.salesmap.kr/mcp
3.  세일즈맵 연결 페이지가 열리면 **API 토큰을 붙여넣고 \[연결 승인]**<br>

    <figure><img src="../.gitbook/assets/image (19).png" alt="" width="413"><figcaption></figcaption></figure>
{% endtab %}

{% tab title="Claude Code" %}
터미널에서 한 줄:

```bash
claude mcp add --transport http salesmap https://mcp.ai.salesmap.kr/mcp \
  --header "Authorization: Bearer <API_토큰>"
```
{% endtab %}

{% tab title="Codex" %}
터미널에서 두 줄:

```bash
# ~/.zshrc 또는 ~/.bashrc 에 추가 후 터미널 재시작 (토큰을 파일에 남기지 않는 방식)
export SALESMAP_API_TOKEN="<API_토큰>"
```

{% code overflow="wrap" %}
```bash
codex mcp add salesmap --url https://mcp.ai.salesmap.kr/mcp --bearer-token-env-var SALESMAP_API_TOKEN
```
{% endcode %}
{% endtab %}

{% tab title="Antigravity" %}
Antigravity 설정 → **Customizations 탭 → Open MCP Config** 클릭\
(파일 위치: `~/.gemini/config/mcp_config.json`)

```json
{
  "mcpServers": {
    "salesmap": {
      "serverUrl": "https://mcp.ai.salesmap.kr/mcp",
      "headers": {
        "Authorization": "Bearer <API_토큰>"
      }
    }
  }
}
```
{% endtab %}
{% endtabs %}

***

### 3단계: 연결 확인

연결 후 AI에게 이렇게 요청해 보세요:

```
세일즈맵에서 내 정보 조회해줘
```

사용자 정보가 나오면 연결 성공입니다.

***

### 문제 해결

| 증상                 | 해결                                                  |
| ------------------ | --------------------------------------------------- |
| "토큰이 유효하지 않습니다"    | 세일즈맵에서 토큰 다시 복사해 넣습니다. 토큰 앞뒤 공백을 제거 후 재시도합니다.       |
| ”npx를 찾을 수 없습니다”   | Node.js 설치를 확인합니다. (20버전 이상 필요)                     |
| "허용되지 않은 IP"       | 워크스페이스에 IP 접근 제한이 있는 경우로, 관리자에게 IP 허용 목록 확인을 요청합니다. |
| AI가 세일즈맵 도구를 찾지 못함 | AI 클라이언트를 재시작합니다. 설정 파일 문법에 문제 없는지 확인합니다.           |
| 도구 호출 시 타임아웃       | 네트워크 연결 상태를 확인합니다.                                  |

***

문의: 세일즈맵 [채널톡](https://salesmap.channel.io/home)으로 연락해주세요.
