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
