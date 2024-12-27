# **OSEK/VDX**

**차량용 RTOS 표준화 단체 및 표준 규격**

### 주요 기능

|                                           |                                                                                                                                               |
| ----------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------- |
| **Task 관리**                               | **OS에 의해 관리되는 단위 프로그램의 제어**                                                                                                                   |
| **Evnet 처리**                              | **Task간 수행 순서 동기를 맞추기 위하여, 지정된 Event 발생까지 Task를 Waiting 시키는 메커니즘**                                                                            |
| **Resource 관리**                           | **서로 다른 우선순위를 가진 task간 공유 자원에 접근을 동기화 시키니 위한 제어 서비스**                                                                                         |
| **Interrupt 처리**                          | **ISR의 두가지 타입 ( Category1, Category2 ) 에 따른 인터럽트 처리 기능 제공**                                                                                   |
| **Alarms 처리**                             | **지정된 시간에 지정된 기능을 수행**                                                                                                                        |
| **Error 처리**                              | **발생한 에러에 대한 정보를 전달하고 사용자가 에러를 처리할 수 있는 Hook 매커니즘 제공**                                                                                        |
| **System  <br>Start-up / Shutdown  <br>** | **시스템 초기화 및 종료에 대한 표준화된 방식을 제공**                                                                                                              |
| **Hook 루틴**                               | **OS 내부 프로세싱 중에 사용자가 정의된 행동을 수행할 수 있도록 OS에서 제공하여 주는 루틴  <br>→ Pre Task Hook, Post Task Hook, Error Hook, Start-up Hook, Shutdown Hook  <br>** |

## Task

**OS가 제어하는 프로그램의 기본 단위**

**\#Task State Model → Task는 실행되면서 상태가 변한다.  
OSEK에서는 2 타입의 Task 상태에 대한 model을 제공 : Basic Task, Extended Task  
**

  

**Basic Task에 대한 State**

![[image 10.png|image 10.png]]

**running : CPU에 할당된 상태, instruction수행, 하나의 task만이 running에 있을 수 있다.**

**ready : running전 우선 stae, scheduler는 ready state에 있는 task 중 다음 에 실행할 task를 결정**

**suspended : 휴식 상태, activated가 가능**

  

  

**Extended Task에 대한 state**

![[image 1 3.png|image 1 3.png]]

**Wait : 특정 event가 발생하기 전까지 동작하지 않는 상태가 추가  
system service에 의해 발생, 동작을 이어가려면 event가 발생해야  
**

  

### Scheduling

OS가 CPU를 사용하려고 하는 프로세스들 사이의 우선순위를 관리하는 작업  
⇒  
**자원을 어떤 프로세스에 얼마나 할당하는지 정책을 만드는 것이라 볼 수 있음.**

  

**Priority 기반의 Scheduling  
1. ready/running state상의 모든 task검색  
2. Highest priority를 가진 task 집합 결정  
3. 그 중에서 가장 먼저 들어온 task 찾아서 Running 상태로 전송  
**

  

### PreTaskHook / PostTaskHook

**TaskHook → 디버깅이나 타이밍 정보를 측정 등 위하여 Task 동작 전후로 사용자가 작성하여 사용할 수 있는 루틴**

**: 동작 방식 :  
순서 : PreTaskHook → Task running → PostTaskHook  
running state 들어간 직후 PreTaskHook 동작  
running state 에서 나오기 직전에 PostTaskHook동작  
TaskHook 동작시 Task의 상태는 Running 상태를 유지  
TaskHook 내에 사용자 루틴을 작성  
**

![[image 2 3.png|image 2 3.png]]

## Event

**Waiting state를 지원하는 task에 대하여 task간 동작 순서를 동기화할 수 있는 mechanism 제공  
⇒ 동작 순서를 동기화하기 위해 사용  
**

**  
Event mechanism  
**

**running state의 extended task는 지정된 이벤트가 발생할 때까지 wait에서 대기  
Waiting state의 extended task는 대기하고 있던 최소 한 개의 이벤트가 발생하면 ready로 전이  
이벤트가 이미 발생된 상태에서 동작중인 extended task가 해당 이벤트를 wait하는 경우 running유지  
**

## Interrupt

**주변 장치에서 발생한 상태 변화  
Interrupt는 Task를 선점한다 : Context switching 발생  
**

  

**분류  
Category 1 Interrupt  
OS 서비스를 사용하지 않는 ISR(Interrupt Service Routine)  
ISR이 끝난 후 직전에 처리 중이던 구문을 계속 처리  
인터럽트가 Task관리에 영향을 주지 않은  
ISR이 최소한의 오버헤드를 가짐  
**

**Category 2 Interrupt  
OS서비스를 사용하는 ISR  
OS가 지정된 사용자 routine를 위하 런타임 환경을 제공하는 ISR-frame을 제공함  
system generation 중에 사용자 루틴이 interrupt에 해  
**

![[image 3 3.png|image 3 3.png]]

## Alarm

**Counter에 기반하여, 특정 시점에 도달했을 경우 지정된 동작을 함으로써 반복적인 이벤트를 발생시킬 수 있도록 하는 OS의 객체**

  

**동작**

**ALARM은 COUNTER가 미리 정의된 값에 도달했을 경우 expire되고, 동작이 가능**

## Resource

컴퓨터 시스템에서 프로그램이나 프로세스가 작동하는데 필요한 다양한 자원을 말한다.

OSEK에서 Resource는 RTOS의 공유 자원을 의미한다. OSEK는 자동차 제어 시스템에서 여러 작업들이 동시에 실행될 때, 자원을 안전하고 효율적으로 관리하기 위해 정의된 표준이다.

- 비유
    
    ### 공장 작업장에서의 비유
    
    ### 1. **작업(task)**:
    
    공장에서 일을 처리하는 여러 **작업자**들이라고 생각하면 돼요. 이 작업자들은 각각의 일을 수행하고 있는데, 작업을 하다가 특정 기계나 도구(리소스)가 필요할 때 그 기계를 사용할 수 있어야 해요.
    
    ### 2. **공유 자원(resource)**:
    
    작업장에서 **공유하는 도구나 기계**와 같아요. 예를 들어, 절단기나 용접기 같은 중요한 기계들이 있죠. 여러 작업자가 이 기계를 동시에 사용하려고 하면 문제가 생길 수 있기 때문에, 작업자들이 서로 순서를 지켜 사용해야 해요. OSEK에서 리소스는 바로 이런 **공유 자원**을 의미해요.
    
    ### 3. **자원 할당 규칙**:
    
    OSEK에서는 작업들이 자원을 사용할 때 **우선순위**를 정해줍니다. 이를 **Priority Ceiling Protocol(우선순위 천장 프로토콜)**이라고 해요. 이 프로토콜을 통해 자원이 충돌 없이 안전하게 사용될 수 있도록 관리하죠.
    
    비유하자면, 공장의 관리자(OSEK 시스템)는 특정 기계를 사용하는 작업자의 우선순위를 미리 정해 놓고, 기계가 사용 중일 때 다른 작업자가 그 기계를 기다리도록 하는 방식이에요.
    
    ### 4. **자원 보호**:
    
    만약 작업자 A가 절단기를 사용하는 동안 작업자 B가 이를 사용하려고 하면, OSEK 시스템은 B가 기다리게 하고 A가 절단기를 다 사용할 때까지 B를 대기시켜요. 이를 **리소스 잠금(locking)**이라고 부릅니다. 작업자 A가 기계를 다 사용하면 **리소스 해제(unlock)**가 이루어지고, 그제서야 작업자 B가 기계를 사용할 수 있어요.
    
    ### 5. **우선순위 역전 방지**:
    
    우선순위가 높은 작업자가 낮은 작업자 때문에 기계를 사용하지 못하면 문제가 생기죠. 이를 방지하기 위해 **우선순위 역전 현상(priority inversion)**이 발생하지 않도록 조정합니다.
    
    비유하자면, 낮은 우선순위의 작업자가 기계를 사용할 때, 높은 우선순위 작업자가 기다리고 있다면 낮은 우선순위 작업이 빨리 끝나도록 도와주는 방식이에요.
    

**우선순위가 다른 여러 task가 공유된 자원에 병행접근 하는 것을 조정 ( 임계영역 보호 )  
Multi-Core 간에는 사용할 수 없음  
**

  

**종류**

1. **Standard  
    GetResource(ResID) - Resource 를 획득하는 API  
    ReleaseResource(ResID) - Resource 를 반환하는 API  
    **
2. **Internal  
    GetResource(ResID), ReleaseResource(ResID) 사용불가  
    Task가 running 상태에 진입할 때 자동 획득  
    Non preemptive scheduling의 rescheduiling의 지점에서 자동으로 release  
    동작은 standard와 같음  
    **
3. **Linked  
    Resource에 대한 nesting 점유는 불가  
    **

![[image 4 3.png|image 4 3.png]]

![[image 5 3.png|image 5 3.png]]

### **제약사항**

**동일 Resource에 대해 중첩해서 획득할 수 없음  
Task/ISR는 점유된 리소스를 가지고 종료할 수 없음  
한 개의 Task에서 다중 리소스를 점유한 경우, 사용자는 LIFO방식으로 리소스를 request/release  
resource를 사용하는 task의 우선순위는 resource에 할당된 우선순위보다 크지 않아야함  
**

## Error Handling

![[image 6 3.png|image 6 3.png]]

![[image 7 2.png|image 7 2.png]]

## System Start-up / Shutdown

### System Start-up

**시스템을 generation할 때 자동으로 시작하는 task와 alarm을 설정**

**StartupHook routine을 제공하여 사용자가 device driver 등을 초기화 할 수 있어야 함**

### Shutdown

**Fatal error 발생 시 application이나 OS에서 Shutdown을 요청**

**ShutdownOS 수행시 ShutdownHook를 호출하고 이 Hook이 종료되면 shutdown을 진행**

  

# AUTOSAR OS

## Schedule Table

**고정적으로 정의되어 있는 expiry point들의 집합**

**지정된 Offset이 지나 Expiry point에 도달하게 되면 각 expiry point에 정의된 Action을 수행  
지정된 duration 내에서 각각의 expiry point를 실행 ( 반복 수행 가능 )  
**

  

![[image 8 2.png|image 8 2.png]]

==기능을 지원하지 않음???==

## Stack Monitoring

**Stack이 설정된 값보다 초과되어 사용되고 있지 않은지 검사 ( Overflow )  
대상 :  
**==**Task, Category 2 ISR  
  
**==**검사 지점 - context switching time**

## Protection Hook

**OS에 의해 감지되는 심각한 에러의 발생을 알리기 위한 Interface 채널  
심각한 에러가 발생했을 때 OS에 의해 호출 ( 내용은  
**==**User에 의해 작성**== **)**

  

**Autosar OS에서 분류한 종류**

|**에러 분류**|**내용**|**ProtectionHook ( 함수 인자 )**|
|---|---|---|
|**Stack Fault**|**Stack이 overflow, underflow**|`**E_OS_STACKFAULT**`|
|**Timing Protection**|**Task/ISR의 수행시간이 정해진 값보다 긴 경우**|`**E_OS_PROTECTION_TIME**`|
||**Task/ISR이 너무 잦은 빈도로 스케쥴링 되는 경우**|`**E_OS_PROTECTION_ARRIVAL**`|
||**resource를 너무 오래 점유**|`**E_OS_PROTECTION_LOCKED**`|
|**Instruction Exception**|**명령어 오류 발생시 ( e.g. divide by zero )**|`**E_OS_PROTECTION_EXCEPTION**`|
|**Memory Protection**|**권한 없는 메모리 영역 접근**|`**E_OS_PROTECTION_MEMORY**`|

**ProtectionHook의 설정 여부에 따라 에러 처리 메커니즘을 가진다**

**설정 X : OS 는 ShutdownOS 호출  
설정 O : OS는 ProtectionHook을 호출하여 아래의 5가지 옵션 중 하나를 선택하도록 한다.  
**

```C
ProtectionReturnType ProtectionHook( StatusType Fatalerror ){
	
	/* Some code */
	
	return PRO_IGNORE;                      // 아무 일도 하지 않음
	return PRO_TERMINATETASKISR;            // 문제가 발생한 TASK/ISR 종료
	return PRO_TERMINATEAPPL;               // 문제가 발생한 TASK/ISR이 속한 OS-Application 종료
	return PRO_TERMINATEAPPL_RESTART;       // 문제가 발생한 TASK/ISR이 속한 OS-Application 재 시작
	return PRO_SHUTDOWN;                    // OS 종료
}
```

  

## Timing Protection

**Task 및 ISR이 지정된 시간에 동작할 수 있도록 timing fault가 발생 시 이에 대한 에러 처리를 수행**

**timing fault는 Task가 deadline을 만족하지 못할 경우 발생  
ㄴ  
**==**Insufficient!! deadline을 만족하지 못한 TASK/ISR이 항상 문제의 원인은 아니다.**==

![[image 9 2.png|image 9 2.png]]

**TASK C는 TASK A 및 B의 지연 때문에 deadline을 만족하지 못함.**

**Autosar 정의 Timing fault**

**Execution Budget - TASK/ISR의 execution time의 상한을 넘겨 수행하는 경우**

**Lock Budget - TASK/ISR이 공유 resource lock / interrupt disalbe로 겪게 되는 blocking time의 상한을 넘는 경우**

**Time Frame - 같은 TASK/ISR이 inter arrival time의 하한보다 짧은 경우 (= 너무 잦은 activation)**

## OS-Application

[참조 링크](https://m.blog.naver.com/techref/222411226439)

**OS object ( Tasks, ISRs, Alarms, Schedul tables, Counters )들 의 모임**

  

## IOC

**OS에 의한 정보 전달 방법  
사용 목적 : 메모리가 보호되는 application 사이에서 communication  
**