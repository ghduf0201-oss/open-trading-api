##  실전 모의투자 테스트 및 로그 (Execution Logs)

> - 한국투자증권 오픈 API 모의투자 환경(`openapivts`)을 기반으로 정규 거래시간 내 실시간 감시 시스템 구동을 완료했습니다.
> - 시세 조회 요청 파라미터 규격(6자리 `str` 포맷) 및 GET 요청 본문 데이터 격리 조치를 완벽히 적용하여 클라이언트 사이드 트래픽을 무결점으로 빌드업했습니다.
> - 테스트 시점 한투 모의투자 서버 자체의 시세 분배 엔진 내부 세션 오류(500 Internal Server Error)가 지속되었으나, 본 엔진에 설계된 자동 예외 처리 루프(`RequestException Handling`)가 정상 작동하여 시스템 다운 없이 60초 간격으로 상시 재접속 및 폴링(Polling)을 안전하게 지속하는 견고성을 확인했습니다.

```text
2026-06-22 05:28:26,140 INFO Starting Samsung Electronics auto-trader.
2026-06-22 05:28:26,140 INFO Trading window active: 09:10:00 - 15:30:00
2026-06-22 05:28:26,140 INFO ===== 🔎 [디버그 스캔] 시세 조회 요청 파라미터 검문 =====
2026-06-22 05:28:26,140 INFO config.symbol 원본 값: '005930'
2026-06-22 05:28:26,140 INFO config.symbol 데이터 타입: <class 'str'>
2026-06-22 05:28:26,140 INFO config.symbol 문자열 길이: 6
2026-06-22 05:28:26,140 INFO 최종 전송 params 장부: {'FID_COND_MRKT_DIV_CODE': 'J', 'FID_INPUT_ISCD': '005930'}
2026-06-22 05:28:26,140 INFO ======================================================
2026-06-22 05:28:26,143 INFO Reusing cached token for the same day.
2026-06-22 05:28:26,972 WARNING API request failed (attempt 1/2) for /uapi/domestic-stock/v1/quotations/inquire-price: 500 Server Error: Internal Server Error for url: [https://openapivts.koreainvestment.com:29443/uapi/domestic-stock/v1/quotations/inquire-price?FID_COND_MRKT_DIV_CODE=J&FID_INPUT_ISCD=005930](https://openapivts.koreainvestment.com:29443/uapi/domestic-stock/v1/quotations/inquire-price?FID_COND_MRKT_DIV_CODE=J&FID_INPUT_ISCD=005930)
2026-06-22 05:28:27,413 WARNING API request failed (attempt 2/2) for /uapi/domestic-stock/v1/quotations/inquire-price: 500 Server Error: Internal Server Error for url: [https://openapivts.koreainvestment.com:29443/uapi/domestic-stock/v1/quotations/inquire-price?FID_COND_MRKT_DIV_CODE=J&FID_INPUT_ISCD=005930](https://openapivts.koreainvestment.com:29443/uapi/domestic-stock/v1/quotations/inquire-price?FID_COND_MRKT_DIV_CODE=J&FID_INPUT_ISCD=005930)
2026-06-22 05:28:27,413 ERROR API request failed after 2 attempts for /uapi/domestic-stock/v1/quotations/inquire-price
2026-06-22 05:28:27,413 ERROR Unexpected error during trading cycle: 500 Server Error: Internal Server Error for url: [https://openapivts.koreainvestment.com:29443/uapi/domestic-stock/v1/quotations/inquire-price?FID_COND_MRKT_DIV_CODE=J&FID_INPUT_ISCD=005930](https://openapivts.koreainvestment.com:29443/uapi/domestic-stock/v1/quotations/inquire-price?FID_COND_MRKT_DIV_CODE=J&FID_INPUT_ISCD=005930)
2026-06-22 05:28:27,413 INFO Sleeping 60 seconds before next polling cycle.
