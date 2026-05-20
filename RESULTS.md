# Results

## 1. 실험 요약
- 저장소: bench-atomics-and-memory
- 커밋 해시: 7f668b0
- 실험 일시: 2026-05-20T15:36:10.896Z -> 2026-05-20T15:36:13.107Z
- 담당자: ai-webgpu-lab
- 실험 유형: `benchmark`
- 상태: `success`

## 2. 질문
- 고정 histogram, scatter accumulation, reduction fixture에서 contention과 memory bandwidth를 함께 비교할 수 있는가
- 하나의 benchmark result에서 winner selection, peak items, shared memory, atomic passes, conflict/bandwidth가 같은 결과 스키마로 기록되는가
- 실제 WGSL atomics 및 memory kernels로 교체하기 전 deterministic atomics benchmark protocol을 고정할 수 있는가

## 3. 실행 환경
### 브라우저
- 이름: Chrome
- 버전: 147.0.7727.15

### 운영체제
- OS: Linux
- 버전: unknown

### 디바이스
- 장치명: Linux x86_64
- device class: `desktop-high`
- CPU: 16 threads
- 메모리: 32 GB
- 전원 상태: `unknown`

### GPU / 실행 모드
- adapter: synthetic-webgpu-atomics-suite
- backend: `webgpu`
- fallback triggered: `false`
- worker mode: `worker`
- cache state: `warm`
- required features: ["shader-f16","timestamp-query"]
- limits snapshot: {"maxComputeWorkgroupSizeX":256,"maxStorageBufferBindingSize":134217728,"maxComputeInvocationsPerWorkgroup":256}

## 4. 워크로드 정의
- 시나리오 이름: Atomics and Memory Benchmark
- 입력 프로필: 3-case-atomics-suite
- 데이터 크기: cases=3; winner=ring-buffer-reduce; backend=webgpu; peakItems=262144; maxWorkgroup=256; sharedMemory=48; suite=atomics-memory-suite-v1; automation=playwright-chromium, cases=3; winner=ring-buffer-reduce; backend=webgpu; peakItems=262144; maxWorkgroup=256; sharedMemory=48; suite=atomics-memory-suite-v1; realAdapter=fallback(Benchmark.Suite not available); automation=playwright-chromium
- dataset: atomics-memory-suite-v1
- model_id 또는 renderer: ring-buffer-reduce
- 양자화/정밀도: -
- resolution: -
- context_tokens: -
- output_tokens: -

## 5. 측정 지표
### 공통
- time_to_interactive_ms: 605.3 ~ 1050.1 ms
- init_ms: 0.9 ms
- success_rate: 1
- peak_memory_note: 32 GB reported by browser
- error_type: -

### Compute / Stress
- suite_case_count: 3
- winning_case: ring-buffer-reduce
- bodies_or_particles: 262144
- workgroup_size: 256
- steps_per_sec: 6141.22
- integration_ms: 0.3004 ms
- avg_dispatch_ms: 0.21 ms
- p95_dispatch_ms: 0.34 ms
- atomics_conflict_pct: 14.721 %
- histogram_spill_pct: 3.2 %
- memory_bandwidth_gbps: 93.28 GB/s
- cache_hit_rate_pct: 90.83 %
- shared_memory_kb: 48 KB
- backends: webgpu
- fallback states: false

## 6. 결과 표
| Run | Scenario | Backend | Cache | Mean | P95 | Notes |
|---|---|---:|---:|---:|---:|---|
| 1 | Atomics and Memory Benchmark | webgpu | warm | 6141.22 | 0.34 | winner=ring-buffer-reduce, conflict=14.721%, bandwidth=93.28 GB/s |
| 2 | Atomics and Memory Benchmark | webgpu | warm | 6141.22 | 0.34 | winner=ring-buffer-reduce, conflict=14.721%, bandwidth=93.28 GB/s |

## 7. 관찰
- atomics and memory benchmark는 backend=webgpu, fallback_triggered=false로 기록됐다.
- compute summary는 steps_per_sec=6141.22, atomics_conflict_pct=14.721, memory_bandwidth_gbps=93.28였다.
- atomics memory metadata는 cases=3; winner=ring-buffer-reduce; backend=webgpu; peakItems=262144; maxWorkgroup=256; sharedMemory=48; suite=atomics-memory-suite-v1; automation=playwright-chromium로 남았다.
- playwright-chromium로 수집된 automation baseline이며 headless=true, browser=Chromium 147.0.7727.15.
- 실제 runtime/model/renderer 교체 전 deterministic harness 결과이므로, 절대 성능보다 보고 경로와 재현성 확인에 우선 의미가 있다.

## 8. Real Adapter vs Deterministic
- adapter: real=bench-atomics-atomics-and-memory-214, deterministic=deterministic-renderer-shootout
- adapter_run: real=connected, deterministic=deterministic
- success_rate: real=1, deterministic=1

## 9. 결론
- atomics 및 memory 비교 실험으로 넘어가기 전 contention-heavy benchmark와 결과 문서가 연결됐다.
- 다음 단계는 deterministic score surface를 실제 WGSL histogram, scatter accumulation, reduction kernels로 교체하되 conflict/bandwidth/shared-memory metric 구조를 유지하는 것이다.
- 이후 texture streaming benchmark와 compute regression suite의 memory stress 기준 입력으로 재사용할 수 있다.

## 10. 첨부
- 스크린샷: ./reports/screenshots/01-atomics-and-memory-benchmark.png, ./reports/screenshots/10-atomics-and-memory-real-atomics-bench.png
- 로그 파일: ./reports/logs/01-atomics-and-memory-benchmark.log, ./reports/logs/10-atomics-and-memory-real-atomics-bench.log
- raw json: ./reports/raw/01-atomics-and-memory-benchmark.json, ./reports/raw/10-atomics-and-memory-real-atomics-bench.json
- 배포 URL: https://ai-webgpu-lab.github.io/bench-atomics-and-memory/
- 관련 이슈/PR: -
