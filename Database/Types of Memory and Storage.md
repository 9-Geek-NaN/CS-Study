![image](https://github.com/user-attachments/assets/fd2b131d-a0da-4ee3-b70f-cb4af199ec40)

# 1. 메모리 (Memory)

## (1) RAM (Random Access Memory)

특징

- 읽기, 쓰기가 가능하며 속도가 빠름
- 휘발성 메모리로 전원이 꺼지면 데이터가 사라짐

종류

- DRAM (Dynamic RAM)
- SRAM (Static RAM)

### (1)-1. DRAM (Dynamic RAM)

- 데이터를 저장하기 위해 축전기를 사용
    - 축전기(Condensator, Capacitor) : 전기를 저장하는 전자 부품. **작은 전기를 모아두는 저장소** 역할
- 주기적인 **데이터 새로고침이 필요**
    - 축전기에 저장된 전하가 시간이 지나면 서서히 줄어들기 때문에, 주기적으로 **데이터를 새로 고침(Refresh)**해야함
- SRAM보다 느리지만 **비용이 저렴**하고 **용량이 큼**

하위 유형

- **SDRAM (Synchronous DRAM)** : 클록 신호(CPU와 메모리 컨트롤러가 서로 데이터를 주고받을 때 **동기화된 타이밍**을 제공하는 신호)에 동기화되어 작동
- **DDR SDRAM (Double Data Rate SDRAM)**
    - 데이터 전송 속도를 두 배로 늘림
    - `DDR4` : 현재 널리 사용되는 표준
    - `DDR5` : 최신 표준으로 속도와 효율성이 향상됨
    - **DDR4**와 **DDR5**가 모두 널리 사용되고 있지만, **DDR4가 여전히 더 많이 사용되고 있음**
        - DDR4가 가격이 상대적으로 저렴
        - DDR5를 사용하려면 DDR5를 지원하는 최신 메인보드와 CPU가 필요
        - DDR4가 시장 보급률 높음
- **GDDR SDRAM (Graphics DDR SDRAM)**
    - 그래픽 처리를 위해 설계된 메모리
    - GPU (Graphics Processing Unit)에 사용

### (1)-2. SRAM (Static RAM)

- 데이터를 저장하기 위해 정적인 플립플롭 구조 사용
- **CPU 캐시**로 사용되며, 속도가 매우 빠름
- DRAM보다 빠름 : 주기적인 데이터 새로고침이 필요하지 않다
- **가격이 비싸고 용량이 작음**
- 사용 사례
    - CPU L1, L2, L3 캐시
    - 소형 고속 메모리 구성 요소

## (2) ROM (Read-Only Memory)

- **읽기 전용 메모리**로 **데이터를 변경할 수 없음**
- **비휘발성 메모리**로 전원이 꺼져도 **데이터가 유지**됨

### (2)-1. Firmware

- 하드웨어를 제어하기 위한 영구 소프트웨어
- 예: 임베디드 시스템, 프린터 펌웨어

### (2)-2. BIOS (Basic Input/Output System)

- 컴퓨터가 부팅될 때 하드웨어 초기화와 OS 로드를 담당

# 2. Storage

![image](https://github.com/user-attachments/assets/419a487b-0c34-445d-823b-831bf9f73bc7)


## (1) HDD (Hard Disk Drive)

- 회전하는 자기 디스크에 데이터 저장
- 용량이 크고 저렴하지만 속도가 느림
- 기계적인 부품(회전 디스크, 읽기/쓰기 헤드 등 기계적 부품)이 있어 충격에 약함
- 사용 사례 : 대용량 데이터 저장, 예산 제한 환경

## (2) SSD (Solid State Drive)

- 플래시 메모리를 사용해 데이터를 저장
- 속도가 빠르고 내구성이 높음
- 기계적 부품이 없어(플래시 메모리 칩, 컨트롤러 등 전자 부품 사용) 충격에 강함
- 사용 사례 : 운영 체제, 고성능 애플리케이션

> **플래시 메모리❓**
>
>**비휘발성 메모리**의 한 종류로, 전원을 꺼도 데이터를 유지할 수 있는 저장장치
>
>전자적으로 데이터를 읽고 쓰며, **반도체 기반**으로 설계되어 있다.
> 

## (3) USB Drive

- 플래시 메모리 기반의 휴대용 저장 장치
- 소형이고 사용이 편리하며 여러 기기에서 호환 가능
- 사용 사례 : 파일 전송, 백업

## (4) SD Card

- 소형 플래시 메모리 카드
- 디지털 카메라, 스마트폰, 태블릿 등에서 사용
- 사용 사례 : 멀티미디어 파일 저장, 확장 가능한 스토리지

# 참고
https://github.com/ByteByteGoHq/system-design-101/?tab=readme-ov-file#types-of-memory-and-storage
