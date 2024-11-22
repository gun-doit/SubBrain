# ⭐⭐⭐⭐⭐

### Event

![[image 6.png|image 6.png]]

### Access Point

![[image 1 2.png|image 1 2.png]]

  

## Software Componet Description

> [!important]  
> 소프트웨어 컴포넌트를 구성하고 설계한 정보를 담고있는 문서Virtual Functional Bus (VFB) level : 최상위 단계컴포넌트 및 컴포넌트 간의 연결을 기술 ( Port, Interface )컴포넌트의 통신 속성 및 서로의 관계 표현구성 요소 : Component, Composition, Port, Interface, Assembly/Delegation ConnectorRun-Time Environmnet (RTE) level : 중간 단계컴포넌트의 행동(Internal Behavior) 기술구성 요소 : Runnable, Event, Access PointImplementation level : 최하위 단계Internal Behavior 구현 ( Runnable 코드 작성 )구성 요소 : Code  

## VFB - Virtual Functional Description

### **Component**

**VFB수준에서 시스템을 구성할때 사용되는 중심 구성 요소  
컴포넌트 간의 상호 작용을 위해  
**==**Port**== **소유  
Port는 정확히 하나의 컴포넌트에 속하며, 컴포넌트와 다른 컴포넌트 간의 상호 작용을 하는 지점  
**

### **Component-type & Component-prototype**

**Component-type : 컴포넌트의 속성을 정의 ( e.g. 특정 기능을 하는 포트를 소유 )  
Component-prototype : Component-type에 대한  
**==**인스턴스( 메모리 할당 )**==

![[image 2 2.png|image 2 2.png]]

### Component-type의 종류

**Application SWC - AUTOSAR의 모든 통신 방법과 서비스를 사용 가능하며 ECU 하드웨어와 독립  
Composition SWC - SW-C간의 집합을 캡슐화 하여, 내부는 숨기고 상위 레벨의 작업 생성  
Service SWC - BSW 모듈과 통신, 표준화된 서비스를 표준화된 인터페이스를 통해 제공  
Sensor-Actuator SWC - 센서나 액추에이터를 제어, Application SWC와 ECU-Abs(IO)사이 통신  
Parameter SWC - 파라미터 값(고정 데이터, 상/변수) 제공, 고정, 캘리브레이션 데이터 접근 허용  
Service Proxy SWC - 모드를 시스템 전체에 분포, ECU는 이 SWC 인스턴스에 대한 복사본 소유  
ECU-Abs SWC - ECU의 특정 IO기능에 접근, C/S 통신의 P-Port제공, Sensor-Actuator SWC와 통신  
NV Block SWC - 비휘발성 데이터에 대한 접근, 비휘발성 데이터와 데이터블록을 할당, NvM 모듈과 통신  
**

---

### Composition

**다른 컴포넌트를 포함하는 컴포넌트  
컴포넌트는 Composition 내에서 Component-prototype으로 존재  
Componet-type에 대한 Component-prototype, Port, Connector를 소유  
Composition도 Componet-type이기 때문에 다른 Composition내에 Component-prototype으로 속할 수 있음  
Root Composition에서 Root Composition Prototype으로 최종적으로 Prototype  
**

![[image 3 2.png|image 3 2.png]]

---

### PORT

**컴포넌트 간의 사호 작용 (통신)을 위한 지점  
P-Port (Provide)와 R-Port (Require)가 있다.  
**

### Interface

**Port가 제공하거나 요구하는 타입을 정의**

![[image 4 2.png|image 4 2.png]]

## Interface의 종류

![[image 5 2.png|image 5 2.png]]

$\color{\#000}\colorbox{\#EEE}{\textsf{Client-Server Interface}}$﻿**  
클라이언트는 서버에게 서비스 수행을 요청하는 것으로 통신을 시작  
서버는 클라이언트로부터 요청을 대기하다가 요청된 서비스를 수행하고 응답  
서비스를 개시하는 방향으로 SWC가 Client인지 Server인지 결정  
**

$\color{\#000}\colorbox{\#EEE}{\textsf{Sender-Receiver Interface}}$﻿**  
컴포넌트 간 시그널 ( Data Element )의 송신과 수신으로 구성, 단방향  
R-Port를 통해 데이터를 받고 , P-Port를 통해 보낸다  
**

$\color{\#000}\colorbox{\#EEE}{\textsf{Mode Switch Interface}}$﻿**  
모드 간의 전환을통해 Runnable을 시작  
Runnable의 시작 방법에 대해 특정 모드에서 Disable/Enable한다.  
모드 매니저는 모드 스위치를 통해 모드를 조정, 모드 유저는 해당 모드를 수신한다.  
**

$\color{\#000}\colorbox{\#EEE}{\textsf{Trigger Interface}}$﻿**  
SWC가 다른 SWC의 실행을 작동  
**

$\color{\#000}\colorbox{\#EEE}{\textsf{Parameter Interface}}$﻿**  
상수 데이터, 고정 데이터, 캘리브레이션 데이터를 컴포넌트에서 사용할 수 있도록 제공한다  
**

$\color{\#000}\colorbox{\#EEE}{\textsf{Nv Data Interface}}$﻿**  
비휘발성 데이터에 대한 접근을 제공한다 → 미지원기능  
**

---

### Assembly Connector

**컴포넌트의 P-port와 R-port가 통신하기 위해 연결  
일반적으로 두 Port는 같은 Interface 속성을 가진다  
**

### Delegation Connector

**Composition을 구성할 때 내부의 Port를 외부에서 사용하기 위해 연결  
P-Port는 P-Port와 R-Port는 R-Port와 연결  
**

![[image 6 2.png|image 6 2.png]]

## RTE - RunTime Environment

### Runnable

**컴포넌트의 실제 구현을 구성하는 가장 작은 단위  
RTE를 통해 시작되는 Instruction Sequence  
하나의 컴포넌트에 여러 Runnable 포함 가능  
간단한 알고리즘이거나 복잡한 프로그램을 실행하는 코드 단위  
**

![[image 7.png]]

  

### Event

**Runnable은 RTE에 의해서 실행되며, Runnable의 특정 방식으로 실행될 수 있도록 Event를 지정한다.**

**종류**

![[image 8.png]]

### Access Point

Runnable에서는 RTE가 제공하는 API를 사용하며, Runnable 내에서 사용하려는 API를 Access Point를 통해 지정한다.

![[image 9.png]]

  

---

## ECU Configuration Description

> [!important]  
> 제어기에 대한 설정 정보를 담고 있는 문서RTE ECU Configuration Description소프트웨어 컴포넌트가 제어기에서 동작할 수 있도록 RTE가 코드 생성을 위해 필요한 제어기 관련 설정을 담고 있는 문서