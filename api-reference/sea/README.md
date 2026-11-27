# SeA (AI SDR)

SeA는 세일즈맵의 AI SDR 제품입니다. 이 섹션은 SeA를 외부 서비스와 연동하기 위한 API 문서를 다룹니다.

앞으로 SeA 관련 API는 CRM 엔드포인트와 분리해 이 섹션 아래에 추가합니다.

인증, Base URL, API 버전, Rate limiting처럼 제품과 무관하게 공통으로 적용되는 내용은 [API Reference](../)의 시작하기 섹션을 참고하세요.

## 이용 조건

SeA API 토큰은 워크스페이스 설정 > SeA > API 메뉴에서 SDR 프로필별로 발급합니다. API 요청과 이벤트 웹훅은 유효한 Free(무료 체험) 또는 Enterprise 플랜의 SeA 구독에서 사용할 수 있습니다. Basic·Professional 플랜이거나 SeA 구독이 만료된 상태에서는 토큰 발급, API 요청, 웹훅 등록·발송이 차단됩니다.

## 사용 가능한 API

### SDR 프로필 데이터 조회

- [방문자 목록 조회](sdr/lead-list.md)
- [방문자 상세 조회](sdr/lead-detail.md)
- [대화 목록 조회](sdr/conversation-list.md)
- [대화 상세 조회](sdr/conversation-detail.md)
- [대화 메시지 목록 조회](sdr/conversation-message-list.md)
- [회사 목록 조회](sdr/organization-list.md)
- [회사 상세 조회](sdr/organization-detail.md)

#### 페이지 이동과 오류 처리

- 다음 페이지를 요청할 때는 이전 응답의 `nextCursor`를 수정하지 않고 `cursor`에 그대로 전달하세요. 직접 만든 커서에 초 단위가 빠진 시각이 들어 있으면 `400 Bad Request`가 반환됩니다. 서버가 발급한 커서에는 초 단위가 포함됩니다.
- 유효한 토큰으로 조회하더라도 커서나 경로 ID 형식이 잘못되면, 구독 상태(`403`)나 호출 한도(`429`)를 검사하기 전에 `400 Bad Request`가 반환됩니다. 이 입력 오류는 호출 한도에 포함되지 않습니다.

#### 호출 한도

위 7개 조회 API는 워크스페이스당 10초에 100회로 제한됩니다. 같은 워크스페이스의 여러 SDR 프로필 토큰으로 요청해도 한도를 공유합니다. 조회할 수 있는 데이터는 각 토큰이 속한 SDR 프로필 범위로 제한됩니다.

한도를 초과하면 `429 Too Many Requests`가 반환됩니다. 응답 본문의 `reason`에 초 단위로 안내된 시간만큼 기다린 뒤 다시 요청하세요.
