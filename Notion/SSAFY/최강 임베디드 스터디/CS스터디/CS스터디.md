## 1 WEEK

- **열민이형**
    
    **주제 : OS (operation system)**
    
    운영체제 : 컴퓨터 시스템의 자원을 효율적으로 활용하고, **사용자가 편리하게 사용할 수 있도록 도움**
    
    window, ios, .. 등 → 서로 호환이 잘 이루어지지 않는다.
    
      
    
    1. 프로세스 관리( porcess )  
        프로세스 : 현재 실행중인 프로그램, 프로그램이 메모리를 할당 받는 과정을 프로세스 라고함.  
        멀티 프로세스 : 프로세스 간의 데이터 이동은 불가능→차후의 지식으론 가능  
        스레드 : CPU의 최소 실행 단위  
        
    2. 저장장치 관리
    3. 네트워킹
    4. 디바이스 드라이버
    
    CPU의 작업 처리 방식
    
    동시성 ( Concurrency ) - 문맥교환( ContextSwitching )
    
    → 문맥교환의 이유 - 효율화(미리 끝나는것들이 끝나지않음) , 하드웨어 한계성(무한대로 할 수 없음)
    
    병렬성 - 말그대로 병렬성.
    
    그럼 dom은 운영체제가 아닌가?
    
- **종원이형**
    
    주제 : CPU, 메모리
    
    컴퓨터를 나누면 크게 네가지
    
    CPU, 메모리, [보조기억장치, 입출력장![[Untitled 33.png|Untitled 33.png]]    ![[/Untitled 33.png|Untitled 33.png]]
    
    **ALU 산술연산장치**
    
    ## [모스펫 ( Mosfet )](https://jungwonlab.tistory.c![[Untitled 1 13.png|Untitled 1 13.png]][메모리 영역]]

![[/Untitled 1 13.png|Untitled 1 13.png]]

## 2 WEEK

- **승헌이형**
    
    7계층 - 물리, 데이터, 네트워크, 전송, 세션, 표현, 응용
    
    ### TCP/UDP - 전송 계층 [[TCP](http://www.ktword.co.kr/test/view/view.php?m_temp1=1889)]
    
    1. 전송방식
        1. TCP - 가상회선 패킷교환
            1. 한곳으로만 보냄
        2. UDP - 데이터 그램 패킷 교환
            1. 받던지 말던지 보냄 - 양아치
    
      
    
    ### TCP 연결
    
    1. SYN 과 CLI 시퀀스 번호를 보냄 [ CLI - SER ]
    2. ACK, CLI 시퀀스 번호+1, SER 시퀀스 번호 [ SER- CLI ]
    3. ACK, SER 시퀀스 번호 + 1 [ CLI - SER ]
    
    = 3-way-handshaking
    
      
    
    ### TCP 연결 해제
    
    1. FIN을 보냄 , FIN-WAIT만큼 기다림 [ CLI - SER ]
    2. ACK, FIN [ SER - CLI ]
    3. ACK, FIN-WAIT만큼 기다림 [ CLI - SER ]
    
      
    
    ### TIME WAIT - ( FIN-WAIT .. )
    
      
    
- **송원누나**
- **성표형**
    
    임베디드 : 특수한 목적을 가지고 (제어가 필요한 것) 수행하는 컴퓨터 시스템
    
    특징
    
    1. 제한된 메모리, 전력
    
    펌웨어 - 하드웨어인데 소프트웨어 역할을 가지고 있다.
    
      
    
    **RTOS - 실시간 운영체제**
    
    Hard - 원자력, 화재
    
    Soft - 컴퓨터, 모바일
    
    특징
    
    1. 반응이 빠르다
    2. Deterministic = dt
    
      
    
      
    
    ## Polling
    
    - cpu의 상태를 계속 측
    
    ## Interrupt
    
      
      
    

[[1 WEEK 발표내용]]