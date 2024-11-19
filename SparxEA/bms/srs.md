# Battery Management System (BMS) Software Requirements Specification

## 문서 정보

- 문서 번호: SRS-BMS-2024-001
- 버전: 1.0
- 상태: Draft
- 작성일: 2024-11-16

## 1. 서론

### 1.1 목적

본 문서는 전기자동차용 리튬이온 배터리의 Battery Management System(BMS)에 대한 소프트웨어 요구사항을 정의한다.

### 1.2 범위

- 승용 전기자동차용 리튬이온 배터리 팩의 관리 및 제어
- A-SPICE 기준 준수
- ISO 26262 기능안전 요구사항 준수

### 1.3 참조 표준

- ISO 26262: Road vehicles - Functional safety
- A-SPICE v3.1
- IEC 61508: Functional Safety of E/E/PE Safety-related Systems

### 1.4 용어

| 용어 | 설명 |
|------|------|
| BMS (Battery Management System) | 배터리의 상태를 모니터링하고 제어하는 시스템 |
| ASIL (Automotive Safety Integrity Level) | ISO 26262에서 정의하는 자동차 안전성 등급 (A~D, D가 최고 등급) |
| SOC (State of Charge) | 배터리의 현재 충전 상태를 백분율로 나타내는 지표 |
| SOH (State of Health) | 배터리의 수명 상태를 나타내는 지표로, 초기 용량 대비 현재 용량의 비율 |
| SOF (State of Function) | 배터리의 현재 작동 가능 상태를 나타내는 지표 |
| UDS (Unified Diagnostic Services) | 자동차 진단 통신 프로토콜 표준 |
| MTBF (Mean Time Between Failures) | 시스템의 평균 고장 간격 시간 |
| HIL (Hardware-in-the-Loop) | 실제 하드웨어와 연동하여 수행하는 시뮬레이션 테스트 |
| FMEA (Failure Mode and Effects Analysis) | 잠재적 고장 모드와 영향을 분석하는 방법 |
| AUTOSAR (AUTomotive Open System ARchitecture) | 자동차 소프트웨어 표준 아키텍처 |
| RTOS (Real-Time Operating System) | 실시간 운영체제 |
| MISRA-C | 자동차 산업에서 사용되는 C 언어 코딩 표준 |
| A-SPICE (Automotive SPICE) | 자동차 소프트웨어 개발 프로세스 평가 모델 |

## 2. 기능 요구사항

### 2.1 배터리 모니터링 (SWR-BMS-001)

- **ASIL-C**
- 각 셀의 전압 측정 (200ms 주기)
  - 측정 범위: 2.5V ~ 4.2V
  - 정확도: ±5mV
- 각 셀의 온도 측정 (1초 주기)
  - 측정 범위: -40°C ~ 85°C
  - 정확도: ±1°C
- 배터리 팩 전류 측정 (100ms 주기)
  - 측정 범위: -400A ~ +400A
  - 정확도: ±1A

### 2.2 배터리 보호 기능 (SWR-BMS-002)

- **ASIL-D**
- 과전압 보호: 4.2V 초과 시 차단
- 저전압 보호: 2.5V 미만 시 차단
- 과전류 보호:
  - 충전 시 200A 초과
  - 방전 시 350A 초과
- 과열 보호: 60°C 초과 시 차단
- 저온 보호: -20°C 미만 시 충전 제한

### 2.3 배터리 상태 추정 (SWR-BMS-003)

- **ASIL-B**
- SOC(State of Charge) 추정
  - 정확도: ±5%
  - 갱신 주기: 1초
- SOH(State of Health) 추정
  - 정확도: ±10%
  - 갱신 주기: 1시간
- SOF(State of Function) 계산
  - 갱신 주기: 1초

### 2.4 통신 인터페이스 (SWR-BMS-004)

- **ASIL-B**
- CAN 통신 프로토콜 지원
  - 500kbps 속도
  - ISO 11898 준수
- 진단 통신 지원
  - UDS (ISO 14229) 준수
  - ISO 15765-2 준수

## 3. 비기능 요구사항

### 3.1 성능 요구사항

- CPU 사용률: 평균 50% 미만, 최대 80% 미만
- RAM 사용률: 최대 80% 미만
- 부팅 시간: 2초 이내
- 응답시간: 중요 알람 10ms 이내

### 3.2 신뢰성 요구사항

- MTBF(Mean Time Between Failures): 10년 이상
- Watchdog 타이머 구현
- 오류 검출 및 복구 메커니즘 구현
- 데이터 무결성 검증

### 3.3 안전성 요구사항

- ISO 26262 ASIL-D 요구사항 충족
- Fail-safe 모드 구현
- 중복 센서 데이터 검증
- Error logging 기능

### 3.4 유지보수성 요구사항

- 모듈화된 소프트웨어 구조
- MISRA-C:2012 코딩 규칙 준수
- 상세한 코드 문서화
- 진단 기능 구현

## 4. 제약사항

### 4.1 하드웨어 제약사항

- MCU: 32-bit Automotive Grade
- Flash Memory: 최소 1MB
- RAM: 최소 128KB
- 동작 온도: -40°C ~ 85°C

### 4.2 소프트웨어 제약사항

- AUTOSAR 기반 아키텍처
- RTOS 사용 필수
- 컴파일러: ISO 26262 인증된 컴파일러 사용

## 5. 검증 요구사항

### 5.1 테스트 요구사항

- 단위 테스트 커버리지 90% 이상
- 통합 테스트 시나리오 구현
- HIL(Hardware-in-the-Loop) 테스트 수행
- 환경 테스트 (-40°C ~ 85°C)

### 5.2 검증 방법

- 정적 코드 분석
- 동적 테스팅
- 기능 안전성 분석
- FMEA 분석
