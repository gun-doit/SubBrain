> **Micro Controller Unit**

**집적 회로 안에 프로세서와 메모리, 입출력 버스 등의 최소한의 컴퓨팅 요소들을 내장한 초소형 컨트롤러**

MCU 업계

- STMicroelectronics → 삼성 가전
- Microchip
- NXP
- Texas Instruments
- Renesas → 차량 / 가전

  

  

## Clock의 이해

> **반도체 IC가 동작되기 위해 필수 요소, Tool이 이를 다해결해 준다.**

==**Clock Ocillator (발진기)**==

내장 Ocillator만 쓰지 않는 이유

- 온도 등 농즈 영향으로 클럭이 정확하지 않을 수 있음.
- 특정 부품에 필요한 클럭을 공급해줄 수 있음  
    → 외주 Ocilllator를 사용하여, MCU 내부 Ocillator보다 빠른 속도의 클럭을 발진  
    

  

==**Prescaler ( 분주기 )**==

만약 두 장치에 각각 다른 클럭을 전달해야 한다면 사용한다.

![[Untitled 17.png|Untitled 17.png]]

  

# HAL ( Hardware Abstraction Layer )

하드웨어 추상화 계층

- 소프트웨어에서 하드웨어를 제어하기 위한 인터페이스
- 개발자들은 레지스터 설정을 일일이 알 필요 없이 Hardware를 쉽게 제어할 수 있다.

![[Untitled 1 8.png|Untitled 1 8.png]]

[[NVIC]]