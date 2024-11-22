  

### 임베디드 시스템 - 컴퓨팅 시스템 중, 전용 기능을 수행하도록 만들어진 시스템

- 특정 목적을 가짐

  

HW - CPU, 메모리, **페리퍼럴( Peripheral )**

- **저장장치, 그래픽, 입출력장치, LAN Card, USB interface 등등**

## POSIX

- **OS들이 지원하는 API 들의 표준 규격, IEEE에서 제정**
- **OS가 App에게 제공하는 API들의 표준**
- **System call : 리눅스가 App 개발자들을 위해 제공하는 API**

### CPU의 역할

0, 1로 구성된 명령어를 하나씩 수행하는 장치

Disk에 명령어를 저장해두고 하나씩 빼서 처리

  

  

## Process

- **실행된 프로그램을 의미 - 0, 1로 이뤄진 프로그램이 실행되어 메모리에 적재된 상태**

> **ps -ef**

**UID : 소유자 id**

**PID : 프로세스 id**

**PPID : 부모 프로세스 id**

- **부모와 자식의 관계를 가진다**

  

  

### Htop

  

  

### Process State Machine

![[Untitled 10.png|Untitled 10.png]]

- **R : Running / Runnable**
- **S : Interruptible Sleep**
- **D : Uniterruptible Sleep**
- **T : Stopped**
- **Z : Zombie**

### Process : R - Run

- 프로세스는 기본적으로 Running 상태 이다.
- 1코어 기준으로 하나의 Process가 Running 하며, 나머지 Process 들은 Runnable 상태에 있다.
- **Run Queue - 우선순위 값에 따라 스케쥴러가 먼저 수행할 것을 결정 지을 수 있는 후보들이 존재하는 큐**
- **Run Queue에 있어야 Core 가 수행한다.**
- **Run Queue에서 탈출하는 경우 → I/O 응답 (disk) 대기하거나 종료 신호 발생 시 탈출**

  

### Process : S - Sleep

- **Uninterruptible Sleep ( D ) : 방해 금지, Signal 안 받음**
- **Interruptible Sleep ( S ) : 방해 가능 , Singal 로 종료 가능**
- Process가 중요한 일을 하기 때문에, 끊기지 않아야 한다면 Sleep으로 진입한다.

  

### Process : Z - Zombie

- 프로세스가 죽지 못하고 있다.
- **프로세스의 종료 과정**
    - 프로세스가 종료된다 → State : Zombie로 진입
        - 아직 Process Descriptor가 남아있음
        - 즉, 부모가 Descriptor를 제거 하기 전까지는 자식은 Zombie
    - 프로세스는 부모 프로세스에게 SIGHLD Signal을 보냄
    - 부모 프로세스는 SIGCHLD signal을 받으면, 정해야한다
        1. 자식 프로세스의 자원이 정리될 대까지 기다려야 한다면, wait() System Call 호출 → 커널이 정리
        2. 아니라면, 비동기적으로 자식 프로세스가 종료되는 것을 기다리지 않을 수 있다.

  

  

  

  

## Signal

- Thread / Process에게 정보를 전달하는 신호
- Linux에선 최대 256개의 신호 까지 전달될 수 있다. → 단순 정보를 보낼 때 사용한다.

  

## Interrupt

- **CPU가 동작 중, 하던 일을 멈추고 처리하는 것.**

  

  

## PCB ( Process Control Block)

- **커널이 프로세스를 제어하기 위한 정보를 저장하는 블록**
- **프로세스 Descriptor 라고도 한다.**
- **저장정보**
    - **프로세스 상태 ( State ), PID 등**
    - **프로세스에 대한 다양한 정보들을 보관**
- **CPU가 프로세스에서 작업을 할 때, 어디까지 했는 지를 기록한다.**

  

  

![[Untitled 1 3.png|Untitled 1 3.png]]

  

  

## VAS ( Virtual Address Space )

- 프로세스는 연속적인 메모리 공간을 사용하고 있다고 착각하도록 한다.