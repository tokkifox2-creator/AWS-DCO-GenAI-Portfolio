# 📋 DCO 교육용 샘플 로그 분석 리포트

> **이 리포트는 Python 스크립트를 통해 자동으로 생성되었습니다.**
> DCO 인턴십 직무 이해를 돕기 위한 교육용 샘플 로그 분석 결과입니다.

## 1. 📊 전체 통계 요약

| 항목 | 결과 | 설명 |
| :--- | :--- | :--- |
| **전체 로그 라인 수** | 140 줄 | 분석 대상이 된 전체 데이터 행 수 |
| **경고/치명 로그 수 (WARNING/CRITICAL)** | 3 개 | 즉각 확인이 필요한 장애 경보 레벨 |
| **주요 관심 대상 로그 수** | 6 개 | CRC 오류, 링크 다운, 티켓 에스컬레이션 로그 |

## 2. ⚠️ 심각도(Severity)별 분포

| 심각도 | 발생 횟수 | 비율 |
| :--- | :--- | :--- |
| ERROR | 2 회 | 1.43% |
| INFO | 135 회 | 96.43% |
| WARNING | 3 회 | 2.14% |

## 3. 🏷️ 이벤트(Event) 종류별 발생 빈도

| 이벤트 이름 | 발생 횟수 |
| :--- | :--- |
| Normal heartbeat | 125 회 |
| Ticket opened | 3 회 |
| Ticket escalated | 3 회 |
| Maintenance completed | 3 회 |
| Fan Alert | 1 회 |
| Temperature warning | 1 회 |
| SSD failure warning | 1 회 |
| CRC error 증가 | 1 회 |
| Link Down | 1 회 |
| Link Up | 1 회 |

## 4. 🚨 WARNING / CRITICAL 로그 상세 목록

| 시간 | 장비명 | 심각도 | 이벤트 | 상세 메시지 |
| :--- | :--- | :--- | :--- | :--- |
| 2026-07-03 01:05:00 | `DEMO_CORE_SW_02` | **WARNING** | Fan Alert | Fan module 2 RPM dropped to 15% (Below threshold 20%). IP: 198.51.100.2 |
| 2026-07-03 02:05:00 | `EDU_SRV_R04_N12` | **WARNING** | Temperature warning | Chassis temperature reached 42C (Threshold: 40C). IP: 192.0.2.12 |
| 2026-07-03 03:05:00 | `SAMPLE_TOR_SW_01` | **WARNING** | CRC error 증가 | Interface Gi0/1 CRC error counter increased to 154 within 5 minutes. IP: 192.0.2.1 |

## 5. 🔍 핵심 관심 탐지 이벤트 요약
*(CRC_ERROR, LINK_DOWN, TICKET_ESCALATED 관련 키워드가 포함된 로그입니다)*

| 시간 | 장비명 | 탐지 유형 | 이벤트 | 상세 메시지 |
| :--- | :--- | :--- | :--- | :--- |
| 2026-07-03 01:10:00 | `DEMO_CORE_SW_02` | 🚨 TICKET_ESCALATED | Ticket escalated | Ticket EDU-TKT-2026-0001 escalated to Local Infrastructure Team. |
| 2026-07-03 02:15:00 | `EDU_SRV_R04_N12` | 🚨 TICKET_ESCALATED | Ticket escalated | Ticket EDU-TKT-2026-0002 escalated to DCO Hardware Support. |
| 2026-07-03 03:05:00 | `SAMPLE_TOR_SW_01` | 🔴 CRC_ERROR | CRC error 증가 | Interface Gi0/1 CRC error counter increased to 154 within 5 minutes. IP: 192.0.2.1 |
| 2026-07-03 03:06:00 | `SAMPLE_TOR_SW_01` | ❌ LINK_DOWN | Link Down | Interface Gi0/1 status changed to DOWN. Connection to server lost. |
| 2026-07-03 03:12:00 | `SAMPLE_TOR_SW_01` | 🚨 TICKET_ESCALATED | Ticket escalated | Ticket EDU-TKT-2026-0003 escalated to Onsite Cabling Team. |
| 2026-07-03 03:30:00 | `SAMPLE_TOR_SW_01` | 🔴 CRC_ERROR | Normal heartbeat | System status is healthy. Interface Gi0/1 running with 0 CRC errors. IP: 192.0.2.1 |

## 6. 💡 DCO 교육용 시나리오 학습 가이드
이 로그 분석 결과를 바탕으로 데이터센터 장애 해결 흐름(Incident Management)을 학습해 볼 수 있습니다:

1. **냉각 팬 장애 대응**: `DEMO_CORE_SW_02` 스위치에서 발생한 팬 모듈 RPM 저하 경보(`Fan Alert`)가 발생하여 서비스 요청 티켓(`Ticket opened`)이 발행되고, 상위 부서로 이관(`Ticket escalated`)되어 최종 교체 후 정상화(`Maintenance completed`)되는 일련의 해결 프로세스를 관찰할 수 있습니다.
2. **하드웨어 장애 대응**: `EDU_SRV_R04_N12` 서버의 SSD 마모 경고(`SSD failure warning`)를 감지해 장애 부품을 즉각 무중단 교체(Hot-swap)하고 RAID 복구를 진행하는 과정을 나타냅니다.
3. **물리 네트워크 회선 장애 대응**: `SAMPLE_TOR_SW_01` 탑오브랙 스위치에서 포트 CRC 에러가 증가한 후 포트 링크 다운(`Link Down`)이 발생하고, 물리 광케이블을 교체 및 청소하여 정상 포트 업(`Link Up`) 상태로 복구하는 케이블링 인시던트 시나리오입니다.
