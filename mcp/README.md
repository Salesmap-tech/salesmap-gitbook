---
description: 세일즈맵 MCP를 사용하면 AI가 세일즈맵 CRM 데이터를 직접 조회하고 관리할 수 있습니다.
---

# MCP

### MCP란?

MCP(Model Context Protocol)는 AI 모델이 외부 서비스의 기능을 표준화된 함수 형태로 호출할 수 있게 해주는 프로토콜입니다.

기존에는 AI가 외부 서비스와 연동하려면 각 서비스의 REST API 엔드포인트, 인증 방식, 요청 포맷 등을 개별적으로 구성해야 했습니다. MCP는 이러한 복잡성을 MCP 서버가 내부적으로 처리하고, AI에게는 통일된 도구 호출 인터페이스만 노출합니다.

세일즈맵 MCP 서버를 연결하면, 별도의 API 연동 작업 없이 AI와 대화만으로 CRM 작업을 수행할 수 있습니다.

### 무엇을 할 수 있나요?

세일즈맵을 Claude·ChatGPT 등 AI에 연결하면, 화면을 오가며 클릭할 필요 없이 **대화로 CRM을 다룰 수 있습니다.**



**이런 요청이 가능해집니다:**

"이번 주에 들어온 리드 중에 아직 연락 안 한 곳 정리해줘"

"어제 미팅한 OO 딜에 미팅 내용 노트로 남겨줘"

"지난달 파이프라인별 딜 현황 요약해줘"

"이 엑셀 파일 세일즈맵에 업로드해줘"



자세한 사항은 아래 문서를 참고해주세요.

{% content-ref url="tools.md" %}
[tools.md](tools.md)
{% endcontent-ref %}

### 동작 방식

```
사용자 ↔ AI 클라이언트 ↔ 세일즈맵 MCP 서버 ↔ 세일즈맵 CRM
```

1. AI 클라이언트에서 세일즈맵 MCP 서버를 연결합니다
2. 자연어로 요청하면 AI가 적절한 도구를 선택하여 실행합니다
3. 세일즈맵 API를 통해 실제 CRM 데이터를 조회/생성/수정/삭제합니다

**모든 요청은 사용자 본인의 API 키로 처리되며**, 서버는 키를 저장하지 않습니다. 기존 세일즈맵 권한 체계가 그대로 적용됩니다.

### 지원 AI 클라이언트

현재 MCP를 지원하는 주요 AI 클라이언트:

* Claude
  * Claude 웹(claude.ai)
  * Claude 데스크탑/모바일 앱
  * Claude Code
* ChatGPT
  * ChatGPT 웹(chatgpt.com)
  * Claude 데스크탑/모바일 앱
  * Codex
* Gemini
  * Gemini 웹(gemini.google.com)
  * Gemini 데스크탑/모바일 앱
  * Antigravity
* 기타



설치 방법에 대한 자세한 정보는 아래 문서를 참고해주세요.

{% content-ref url="getting-started.md" %}
[getting-started.md](getting-started.md)
{% endcontent-ref %}
