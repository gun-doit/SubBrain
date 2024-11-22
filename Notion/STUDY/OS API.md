## Event

==**StatusType**== **SetEvent( Task Type <TaskID>, EventMaskType <Mask> )  
- task <TaskID>가 기다리고 있던 event <Mask>라면, task의 state를 waiting에서 ready로 바꿈**

==**StatusType**== **ClearEvent( EventMaskType <Mask> )  
- 현재의 event 발생 해제, 해제하려는 event를 소유하고 있는 task만 사용가능**

==**StatusType**== **GetEvent( TaskType <TaskID>, EventMaskRefType <Mask> )  
- <TaskID>가 가지고 있는 모든 event의 상태 bit를 return함  
**

==**StatusType**== **WaitEvent( EventMaskType <Mask> )  
- non suspended extended task를 wait state로 옮  
**

## Interrupt

==**void**== **EnableAllInterrupt(void) /** ==**void**== **DisableAllInterrupts(void)  
- Enable / Disable all interrupts, Nesting은 허용되지 않음  
**

==**void**== **ResumeAllInterrupts(void) /** ==**void**== **SuspendAllInterrupts(void)  
- Enable / Disable all interrupts, Nesting 허용  
**

==**void**== **ResumeOSInterrupts(void) /** ==**void**== **SuspendOSInterrupts(void)  
- Enable / Disable all interrupts of cat.2, Nesting 허용  
**

`**Nesting**` **: 동일한 API를 중첩하여 호출 하는 것을 의미**

## Alarm

==**StatusType**== **GetAlarmBase( AlarmType <AlarmID>, AlarmBaseRefType <info> )  
- alarm의 기본적인 정보 획득 ( counter의 최대값, counter의 tick, alarm 주기가 가질 수 있는 최소값  
**

==**StatusType**== **GetAlarm( AlarmType <AlarmID>, TickRefType <Tick>)  
- alarm이 expire하기 전까지 상대적으로 남은 tick수 반환  
**

==**StatusType**== **SetRelAlarm( AlarmType <AlarmID>, TickType <Increment>, TickType <Cycle>)  
- 현재 상태에서 increment만큼 tick 증가 후 expire되고, 이 후로 Cycle 주기로 expire되는 알람을 설정  
- cycle이 0일 경우 1회만 알람이 expire됨  
**

==**StatusType**== **SetAbsAlarm( AlarmType <AlarmID>, TickType <Start>, TickType <Cycle> )  
- 처음으로 <Start> tick에 도달한 후 expire되고, 이후로 Cycle 주기로 expire되는 알람을 설정  
- cycle이 0인 경우 1회만 알람이 expire됨  
**

==**StatusType**== **CancelAlarm( AlarmType <AlarmID> )  
- 해당 alarm이 expire되지 않도록 변경  
**

## Resource

**GetResource( ResID ) - Resource를 획득하는 API**

**ReleaseResource( ResID ) - Resource를 반환하는 API**