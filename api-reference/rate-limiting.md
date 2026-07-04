# Rate limiting

### Rate limiting

* 워크스페이스 별로 API 호출 횟수 제한이 있습니다.
* 횟수 제한은 모든 API enpoint 기준이며 100 요청 / 10초 입니다.
* 해당 조건을 초과한 api 호출이 일어날 경우에는 다음과 같은 메시지를 리턴합니다.

```json
// HTTP Status Code 429
{
    "success": false,
    "message": "Too Many Requests"
}
```

### Rate limiting 피하기

* API 요청시 rate limiting 범위를 초과하지 않도록 시간 간격을 설정합니다.
* rate limiting 범위를 넘은 경우 10초 후 다시 API 를 요청합니다.
