# [교육용 샘플] Ticket ID: EDU-TICKET-2026-0001

> [!NOTE]
> **[교육용 샘플 데이터 안내]**
> 본 문서는 교육용 가상 시나리오를 바탕으로 작성된 샘플 데이터이며, 실제 운영되는 장비 정보, AWS 내부 절차, 실제 IP 또는 티켓 데이터와 일절 관련이 없습니다.

## 1. 티켓 정보 (Ticket Summary)
* **티켓 ID**: `EDU-TICKET-2026-0001`
* **발생 시간**: `2026-07-07 15:00:00 KST`
* **대상 장비**: `SAMPLE_TOR_SW_01` (Top-of-Rack Switch)
* **영향 포트**: `SAMPLE_PORT_1/1`
* **이벤트 종류**: `CRC Error Increment & Link Down`
* **심각도 (Severity)**: `SAMPLE_SEV_3` (업무 영향도: 해당 랙 서비스 일부 영향)

## 2. 장애 상황 및 관찰 내용 (Observation Details)
* **이벤트 로그 흐름**:
  1. `14:50:00 KST`: `SAMPLE_PORT_1/1`에서 초당 CRC Error 수치 급증 감지 (5분간 약 15,000개 누적).
  2. `14:55:00 KST`: CRC Error에 따른 패킷 드롭 임계치 초과 경보 발생.
  3. `14:58:30 KST`: `SAMPLE_PORT_1/1` 상태가 `Link Down`으로 변경됨.
* **관찰 내용**:
  * 물리 링크 계층에서 간헐적인 신호 감쇠 및 에러 패킷 누적이 발생한 후, 스위치 포트가 최종적으로 Down 상태로 전송 불능 상태가 됨.
  * 트래픽이 이중화 경로(Redundant Link)인 `SAMPLE_TOR_SW_02`로 자동 우회되어 전체 중단은 모면했으나 대역폭 손실 발생.

## 3. 에스컬레이션 (Escalation Status)
* **Escalation 필요 여부**: **필요 (YES)**
* **지정 대상 팀**: `SAMPLE_NW_INFRA_TEAM` (네트워크 인프라 지원 조직)
* **사유**: `SAMPLE_PORT_1/1` 포트의 물리 케이블(광케이블/트랜시버) 불량 혹은 상위 패치 패널의 물리적 접속 불량 가능성이 높아 현장 점검 및 부품 교체(SFPs)가 요구됨.

## 4. 보안 주의사항 (Security & Compliance)
* 본 문서 및 분석 작업 시 **실제 고객 정보, 실제 IP 주소, 장비 시리얼 번호, AWS 내부 계정 정보 등**의 민감 데이터가 포함되지 않도록 절대 주의해야 합니다.
* 모든 IP 및 장비명은 `SAMPLE_` 또는 `EDU_` 접두어만을 사용하여 가상 정보로 치환하여 처리되어야 합니다.
