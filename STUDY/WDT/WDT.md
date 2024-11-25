[참조 링크](https://gdnn.tistory.com/116#google_vignette)

**Watchdog Timer - 감시견!  
MCU가 고장나서 중단되거나 소프트웨어 오류로  
**==**무한 루프에 빠지는 상태를 감시**==**한다.  
→ 정상동작 하지 않는다고 판단하면 시스템을 리셋시킨다.  
**

  

  

  

### 동작방식

Watchdog의 타이머는 HW를 주기적으로 감시하며 시간을 재는 계수 회로. 디바이스로부터 일정 시간동안 입력값을 받지 못하는 경우 시스템의 오동작 상황으로 간주하고 초기화 진행

  

![[image 29.png|image 29.png]]ge 29.png|ima![[image 1 8.png|image 1 8.png]]mage 1 8.png|image 1 8![[image 2 8.png|image 2 8.png]]
![[/image 2 8.png|image 2 8.png]]

- Watchdog Control Register (WDCR)
    - 와치 독을 컨트롤 하는 레지스터
    - 리셋 상태 설정, 사용여부, 로직 체크
- Watchdog Counter Register (WDCNTR)
    - 와치독 카운터의 상태 레지스터
    - 현재까지 카운팅 된 값 확인 가능
- Watchdog Reset Key Register (WDKEY)
    - 와치독 카운터를 Clear하는 역할
- System Control and Status Register (SCSR)
    - 와치독 카운터 출력 신호 결과를 리셋 /![[image 3 8.png|image 3 8.png]]트웨어

### 동작 방식

![[/image 3 8.png|image 3 8.png]]

  

  

  

---

[https://coder-in-war.tistory.com/entry/Embedded-02-WDT%EC%9B%8C%EC%B9%98%EB%8F%85-%ED%83%80%EC%9D%B4%EB%A8%B8%EB%9E%80](https://coder-in-war.tistory.com/entry/Embedded-02-WDT%EC%9B%8C%EC%B9%98%EB%8F%85-%ED%83%80%EC%9D%B4%EB%A8%B8%EB%9E%80)