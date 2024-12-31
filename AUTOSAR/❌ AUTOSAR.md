- **공부 링크**
    [https://xenostudy.tistory.com/679#google_vignette](https://xenostudy.tistory.com/679#google_vignette)
    [https://autosw.tistory.com/13](https://autosw.tistory.com/13)
    [https://autosw.tistory.com/notice/11](https://autosw.tistory.com/notice/11)
    [AUTOSAR 4.1.1의 최신 기술과 이해 (autoelectronics.co.kr)](https://www.autoelectronics.co.kr/article/articleView.asp?idx=1270#:~:text=%E2%91%A4%20PORT%EB%8A%94%20MCU%EC%9D%98%20%EA%B8%B0%EB%B3%B8%EC%84%A4%EC%A0%95%20%EC%9D%B4%ED%9B%84%EC%97%90%20Board%EC%83%81%EC%9D%98%20Pin%EC%9D%84%20%EC%96%B4%EB%96%A4,%EB%B3%80%EA%B2%BD%EC%9D%84%20%EC%9C%84%ED%95%9C%20API%EB%A5%BC%20%EC%83%9D%EC%84%B1%ED%95%A0%20%EA%B2%83%EC%9D%B8%EC%A7%80%EB%A5%BC%20%EC%84%A4%EC%A0%95%ED%95%98%EB%8A%94%20Device%20Driver%EC%9D%B4%EB%8B%A4.)

> [!important]  
> 차량용 ECU의 특성하드웨어(센어 및 엑추에이터)와 상호 작용 및 통신CAN, LIN, FlexRay or Ethernet 같은 차량 네트워크 통신전력 및 메모리가 제한된 자원을 가진 MCU, RTOS를 사용내부 또는 외부 플래시 메모리에서 프로그램 실행  

- **개발 배경 WHY**
    
    제어기 수량의 증가 및 차량 공간의 제약에 따라 제어기 통합 필요  
    제어기 SW의 복잡성이 증가함에 따라 플랫폼 공용화 및 표준화 필요  
    
- ==**AUTOSAR 소프트웨어 개발 순서**==
    
    1. **Configure System  
        시스템 설정 단계로 컴포넌트의 구성/연결 등을 정의한다 (SCD을 개발)  
    2. **Implement Componet  
        ”Configure System” 단계에서 구성한 컴포넌트들에 대한 코드 구현 등을 진행  
    3. **Extract ECU-Specific Information  
        시스템 구성 정보로 부터 특정 제어기 SW를 구현하기 위한 정보만을 추출  
    4. **Configure ECU  
        제어기 관련 설정을 진행 ( ECU Configuration Description 개발 )  
    5. **Generate Executable  
        제어기에서 동작하는 실행 파일을 생성한다. ( 컴파일 및 링크를 통해 실행 이미지 생성)  
    
    ![[image.png]]
    
      
    
    ### AUTOSAR 개발 과정
    
    1. **일반적으로 Top-down 방식으로 개발**
    2. **시스템 설계자는 VFB 상에서 SW-C를 설계. SW-C간 Data의 이동은 Port와 Interface로 정의**
    3. Configure System이라는 디자인 단계에서 SW-C는 특정 ECU에 할당. ECU Extract과정을 통해 개발 ECU에 설계 정보 전달
    4. 개별 ECU는 SW-C간 또는 SW-C와 BSW간 구체적인 인터페이스를 RTE를 통해 구현

## 오토사 아키텍처

**크게 3개의 계층으로 나뉜다. Application Layer, Runtime Environment(RTE), Basic Software(BSW)**

**다중 프로세스/스레드가 지원되지 않는 임베디드 시스템상에서 구현되고 동작하기 때문에  
  
**==**하위 3개의 계층이 한꺼번에 컴파일되고 링킹**== **되어 타깃에 기록된다.**

  

## AUTOSAR 플랫폼 구조

![[image 1.png]]

## 계층 관점

$\color{\#000000}\colorbox{\#999fff}{\textsf{Service Layer}}$﻿**  
Application에 BSW에서 제공하는 기능을  
**==**서비스 형태**==**로 제공  
대게 모듈명 뒤에  
**==**Manger, Management, ComM ( Communication Manager ) 등**== **접미사 붙음  
주요 서비스 :  
**==**통신 및 채널 관리, 진단, 제어기 상태, Task Scheduling, 비 휘발 생 메모리, 와치독**==

$\color{\#000000}\colorbox{\#00CC99}{\textsf{ECU Abstraction Layer}}$﻿**  
제어기 하드웨어에 종속적이지 않은 일정한 인터페이스를 서비스 및 App계층에 제공  
대게 Interface라는 접미사가 붙음  
  
**==**실제 제어기 하드웨어 구현 시 비활성 메모리인 경우**==**, 컨트롤러 내부 또는 외부 메모리를 사용할 수 있는데 이들은 하위 계층에서 별도의 모듈로 구현되나 상위 계층에선** ==**이 추상화 계층에서 제공하는 단일 인터페이스를 통해 접근 가능**==**함  
주요 서비스 : 통신, 메모리, 입출력, 와치독 Interface  
**

$\color{\#000000}\colorbox{\#FF7C80}{\textsf{Micro-Controller Abstraction Layer}}$﻿**  
흔히 MCAL이라고 불리며 마이크로 컨트롤러에 정속적이지 않은 일정한 인터페이스를 추상화 계층에 제공  
→  
**==**상이한 하드웨어 설계를 가지는 마이크로 컨트롤러 ( Infineon Aurix, NXP MPCxxxx 등 )로 부터 동일한 하드웨어 인터페이스를 추상화 계층에 제공**==

**주요 서비스 : 통신, 메모리, 입출력, 와치독 모듈**

  

## 기능 관점

![[image 2.png]]

1. **시스템 기능  
    운영체제, 각종 매니저( ComM, EcuM 등 ) 모듈이 해당  
    전반적으로 사용되는 서비스를 App과 BSW 모듈에 제공  
    **
2. **메모리 기능  
    NvRAM Manager, MemAbs, Eeprom Abs, Flash Eeprom emulation, Internal/External Flash Driver 등이 해당  
    외부 디바이스의 경우 SPI or I2C driver가 추가적으로 사용  
      
    **==**비회발성 메모리 접근을 제어하기 위한 상태 관리, 읽기/쓰기 인터페이스 제공 그리고 대상 메모리 디바이스 설정 기능 제공**==
3. **통신 기능  
    Communication Manager, State Manager, Com, LdCom, PduR, Transport Module, Interface Module, Driver 모듈이 해당  
    실제 버스(Bus) 상의 하드웨어에서 수신되는 데이터를 애플리케이션에 신호로 전달하기 위한 일련의 과정을 처리  
    **
4. **암호 기능  
    Crypto Service Manager, Key Manager, Crypto HW Abs, Crypto Driver가 해당  
    Crypto Driver의 경우 마이크로 컨트롤러 벤더 별 상이한 이름과 기능을 가지지만 제공되는 인터페이스를 통일하여 호환성을 갖춤  
    주로 SecOC 또는 진단 시 필요한 암호화 기능을 제공  
    **
5. **입출력 하드웨어 기능  
    I/O HW Ab, I/O Driver가 해당  
      
    **==**ADC 신호, PWM신호등 하드웨어에서 전달되는 신호를 App에 제공하기 전 정의된 규격에 따라 신호를 전처리 한 후, 정의된 인터페이스의 형태로 전달**==
6. **진단 및 에러처리 기능  
    Diagnostic Manager, Dignostic Event Manager, Function Inhibit Manager등이 해당  
    **
7. **오프보드 통신 기능  
    V2X management, Facilities, Transport Layer 그리고 V2X Networking 등이 해당  
    기존의 통신 기능에 추가적으로 애드혹 기반의 차대차 또는 차대 사물 통신 기능을 지원  
    **

## SW-C Description

**SWC는 AUTOSAR 개발 도구를 통해 SWCD(ARXML)파일로 생성된다.**

1. **VFB level로 SWC의 기본적인 통신 특성과 다른 SWC** ==**통신 관계**==**를 정의한다.  
    ㄴ 모델화된 통신 구조가 RTE로 구현 되는 것이다.  
    **
    
    ![[image 3.png]]
    
2. **RTE level로 SWC의 간단한 알고리즘이나 프로그램을 실행하는 코드 단위인 Runnable을 생성하고 실행하기 위한 방법인 Event를 설정한다.**
3. **Implementation level에서 SWC의 내부 동작을 Runnable소스 코드를 작성하면 SWC설계가 완료된다.**

![[image 4.png]]

  

## 오토사 제어기 개발 절차

일반적으로…

1. 차량 제조사가 대상 차량 플랫폼의 기능을 시스템 관점에서 설계 및 기술하고 각 제어기 별로 기능 분배 (System Description)
2. 분배된 기능은 각 제어기 별로 추출되어 하나의 독립적인 파일로 기술됨 ( ECU Extract )  
    ㄴ 부품사에서 타깃 제어기 개발을 위한 입력 자료로 사용  
    
3. 부품사에서는 입력 자료를 바탕으로 제어기의 세부 기능을 BSW와 SWC로 나누어 설정 및 설계 함

![[image 5.png]]

  

  

---

[포트와 인터페이스](https://www.autosartoday.com/posts/types_of_interfaces_and_ports)