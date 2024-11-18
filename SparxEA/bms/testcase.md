# Test Cases for Sensor Calibration Scenario

## Test Case Information
- Test Case Group: TC-BMS-CAL
- Related Use Case: UC-BMS-MON-001 Alternate Path 1
- Test Level: Integration Test
- Initial Condition: BMS 정상 동작 상태

## TC-BMS-CAL-001: 정상적인 센서 재보정 절차 검증

### Description
전압 센서의 측정값이 보정 허용 오차를 초과할 때 정상적인 재보정 수행을 검증

### Preconditions
1. BMS 시스템 정상 동작 중
2. 모든 센서가 활성화 상태
3. 기준 전압 소스 연결됨 (3.7V ± 0.1mV)

### Test Steps
1. 전압 센서에 3.7V 기준 전압 입력
2. 센서 측정값 확인 (예상: 3.706V로 측정)
3. 보정 허용 오차(±5mV) 초과 확인
4. 자동 센서 보정 루틴 시작 관찰
5. 보정 과정 완료 대기
6. 보정 후 측정값 확인
7. 진단 로그 데이터 확인

### Expected Results
1. 보정 전 센서 측정값: 3.706V ± 0.1mV
2. 보정 루틴 자동 시작됨
3. 보정 후 센서 측정값: 3.700V ± 0.5mV
4. 진단 로그에 보정 이벤트 기록
   - 이벤트 코드: CAL_EVT_001
   - 보정 전 값: 3.706V
   - 보정 후 값: 3.700V
   - 타임스탬프 존재

### Pass/Fail Criteria
- PASS: 모든 Expected Results 만족
- FAIL: Expected Results 중 하나라도 불만족

## TC-BMS-CAL-002: 다중 센서 동시 재보정 검증

### Description
여러 전압 센서가 동시에 보정이 필요한 상황에서의 재보정 동작 검증

### Preconditions
1. BMS 시스템 정상 동작 중
2. 3개의 인접 전압 센서 선택
3. 기준 전압 소스 연결됨 (3.7V ± 0.1mV)

### Test Steps
1. 3개 센서에 동시에 3.7V 기준 전압 입력
2. 각 센서 측정값 확인
   - 센서 1: 3.708V
   - 센서 2: 3.707V
   - 센서 3: 3.709V
3. 동시 보정 루틴 시작 관찰
4. 보정 완료까지 대기
5. 각 센서의 보정 후 측정값 확인
6. 시스템 부하 상태 모니터링
7. 보정 순서 및 타이밍 기록

### Expected Results
1. 센서 보정이 우선순위에 따라 순차적으로 실행
2. 모든 센서가 120초 이내에 보정 완료
3. 보정 후 모든 센서 측정값: 3.700V ± 0.5mV
4. CPU 부하율 90% 미만 유지
5. 각 센서별 보정 로그 생성

### Pass/Fail Criteria
- PASS: 모든 센서가 정상 보정되고 시스템 부하 기준 충족
- FAIL: 하나 이상의 센서 보정 실패 또는 시스템 부하 초과

## TC-BMS-CAL-003: 보정 실패 후 복구 절차 검증

### Description
센서 재보정 실패 시 시스템 복구 절차의 정상 동작 검증

### Preconditions
1. BMS 시스템 정상 동작 중
2. 테스트 대상 센서 정상 상태
3. 고의적 보정 실패 조건 설정
   - 노이즈 신호 주입: 100mV, 120Hz

### Test Steps
1. 전압 센서에 3.7V 기준 전압 입력
2. 노이즈 신호 주입으로 보정 실패 유도
3. 첫 번째 보정 시도 실패 관찰
4. 시스템의 재시도 동작 확인
5. 세 번의 재시도 후 최종 실패 상태 확인
6. 백업 센서로의 전환 과정 관찰
7. 오류 코드 및 경고 메시지 확인
8. VCU 통신 메시지 모니터링

### Expected Results
1. 보정 실패 후 최대 3회 재시도 수행
2. 실패 후 적절한 DTC 코드 생성
   - DTC: P0A04 (센서 보정 실패)
3. VCU로 경고 메시지 전송 확인
4. 백업 센서로 자동 전환
5. 제한된 동작 모드 진입
6. 실패 이벤트 상세 로깅
   - 실패 시간
   - 실패 원인
   - 재시도 횟수
   - 최종 조치

### Pass/Fail Criteria
- PASS: 모든 실패 처리 절차가 정상적으로 수행
- FAIL: 실패 처리 절차 미흡 또는 백업 전환 실패

## Test Environment Requirements
1. Hardware
   - BMS 테스트 벤치
   - 전압 센서 시뮬레이터
   - 노이즈 발생기
   - 오실로스코프

2. Software
   - BMS 진단 소프트웨어 v2.1 이상
   - 데이터 로깅 툴
   - CAN 모니터링 툴

3. Test Data
   - 센서 보정 기준값 데이터셋
   - 노이즈 패턴 데이터
   - 기대 응답 시간 기준표