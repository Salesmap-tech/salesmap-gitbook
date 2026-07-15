# API Reference

세일즈맵 API Reference는 세일즈맵 제품군을 외부 시스템과 연동하기 위한 API 문서입니다.

문서는 공통 계약과 제품별 엔드포인트를 분리해서 제공합니다.

## 공통

아래 내용은 CRM API와 SeA API에 공통으로 적용됩니다.

* [인증](authentication.md)
* [Base URL 및 버전](api-endpoints.md)
* [Rate limiting](rate-limiting.md)

## 제품별 엔드포인트

* [CRM](crm/README.md): 고객, 회사, 리드, 딜, 노트, 파일, 커스텀 오브젝트 등 CRM 데이터 연동 API
* [SeA (AI SDR)](sea/README.md): AI SDR 위젯, 대화, 리드 수집, 지식 소스 등 SeA 연동 API

새로운 엔드포인트를 추가할 때는 먼저 공통 계약에 해당하는지, 특정 제품 도메인에 속하는지 확인한 뒤 적절한 섹션 아래에 배치합니다.
