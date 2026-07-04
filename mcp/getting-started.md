---
description: 이 문서에서는 Claude Desktop 기준으로 MCP 설치 방법을 설명합니다.
---

# 시작하기

### 사전 준비

* 세일즈맵 계정
* Claude Desktop 설치

### 1단계: API 키 발급

1. 세일즈맵에 로그인합니다
2. **설정 → 연동 → API** 메뉴로 이동합니다
3. **토큰 생성**을 클릭하여 API 키를 발급합니다
4. 생성된 키를 복사해 주세요.

{% hint style="info" %}
키는 발급한 사용자의 권한을 그대로 따릅니다.

가령 읽기 전용 사용자의 토큰으로는 읽기만 가능하며 쓰기 관련 도구는 사용할 수 없습니다.
{% endhint %}

### 2단계: Claude Desktop 설정

Claude Desktop의 MCP 설정 파일을 열어 아래 내용을 추가합니다.

**설정 파일 위치:**

* macOS: `~/Library/Application Support/Claude/claude_desktop_config.json`
* Windows: `%APPDATA%\Claude\claude_desktop_config.json`

{% code overflow="wrap" expandable="true" %}
```json
"salesmap": {
      "command": "npx",
      "args": [
        "-y",
        "mcp-remote",
        "https://salesmap-mcp.vercel.app/api/mcp",
        "--header",
        "Authorization: Bearer <여기에_API_키_입력>"
      ]
    }
```
{% endcode %}

`<여기에_API_키_입력>` 부분을 1단계에서 발급받은 키로 교체하세요.

{% hint style="info" %}
Node.js 20 버전 이상이 설치되어 있어야 합니다.
{% endhint %}

### 3단계: 연결 확인

1. Claude Desktop을 **재시작**합니다
2. 대화를 통해 연결 상태를 확인합니다.

### 첫 대화 해보기

연결이 완료되면 Claude에게 바로 요청해 보세요:

```
세일즈맵에서 내 정보 조회해줘
```

Claude가 `salesmap-get-user-details` 도구를 호출하여 현재 로그인된 사용자 정보를 보여줍니다. 응답이 정상적으로 오면 연결 성공입니다.

다른 요청 예시:

```
딜 파이프라인 목록 보여줘
```

```
고객 중에 "김" 으로 시작하는 사람 검색해줘
```

### 문제 해결

| 증상                         | 해결 방법                        |
| -------------------------- | ---------------------------- |
| Claude가 salesmap 도구를 찾지 못함 | Claude Desktop 재시작. 설정 파일 확인 |
| ”토큰이 유효하지 않습니다”            | API 키가 정확한지 확인. 토큰 앞뒤 공백 제거  |
| ”npx를 찾을 수 없습니다”           | Node.js 설치 확인 (20버전 이상 필요)   |
| 도구 호출 시 타임아웃               | 네트워크 연결 확인                   |
