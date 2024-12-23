> **Inter-Integrated Circuit**

하나는 Data 핀, 다른 하나는 Clcok 핀이다.

**SDA / SCL → 내가 산 부품에 해당 핀이 있다면, I2C 통신이 가능하다.**

Master / Slave라는 용어를 대체로 사용 → Main / Sub라는 용어로 대체중 ㅋ

  

**동작**

**I2C 통신을 하는 장치들은 주소 값을 가진다.**

**→ 장치가 연결되면, 각자 주소 값을 부여 받는다.**

**→ 특정 장치가 어떤 주소에 위치하는지 코드에 넣어야 한다.**

  ![[Untitled 40.png|Untitled 40.png]]40.png|Untitled 40.png]]

1. **여러 개의 슬레이브와 통신이 가능하며, 여러 개의 마스터끼리도 통신이 가능**
2. **데이터를 주고 받는 데** **==두 개의 통신선==****만 필요,** **==SCL, SDA==****라고 한다.**

  

### **특징**

1. **==7비트의 주소 공간==****을 사용하며** **==128개의 Slave==****를 사용가능.**
2. **==여러 개의 마스터끼리 통신이 가능 하며 400Khz의 전송 속도==****를 가짐.**
3. **장치가** **==sleep 모드일 때 주소 인식으로 깨어날 수 있음==****.**

  

### **왜 사용하는가?**

1. ==**UART 통신**====**과 같은**== ==**비동기 통신**==**은 사전에** ==**디바이스 간의 데이터 전송 속도**==**를 맞추어야 한다.  
    → 서로 통신하는 장치들은 오차가 없이 동일한 속도로 데이터를 보내야 하고 조금이라도  
    **==**속도가 맞지 않으면 잘못된 데이터가 송신/수신**== **된다.  
    →  
    **==**비동기 통신은 많은 하드웨어 장치가 요구**==**되며, 매 데이터 마다** ==**시작 비트와 종료 비트를 포함**==**해야 하고 비효율적인 통신 방식임.**
2. ==**SPI 통신**==**은** ==**동기 통신**==**이며 마스터와 슬레이브 간 연결할 때** ==**MISO, MOSI, SCK, CS**== **총 4개의 선이 필요하다  
    → 슬레이브에서 마스터, 마스터에서 슬레이브로 가는 통신선이 존재하여 송**==**신과 동시에 수신이 가능하다는 장점**==**이 있지만 선이 많이 필요하므로** ==**여러 개의 슬레이브를 연결할 때 상당히 복잡**==**하여 사용하기 힘들다.**

### ⇒ I2C 통신은 UART와 다르게 동기 통신이고, SPI와 다르게 SCL, SDA 두가지 선으로 여러 개의 슬레이브![[Untitled 1 15.png|Untitled 1 15.png]]신을 위해 필요한 조건

![[/Untitled 1 15.png|Untitled 1 15.png]]

SDA, SCL 선은 기본 값(디폴트)으로 HIGH인 상태여야 한다. 그러므로 이 두 개의 선이 HIGH인 상태가 되기 위해서는 반드시 버스에 PULLUP 저항을 달아주어야 한다. 각각의 신호선은 PULLUP 저항으로 연결되어 있어서 어떤 장치도 신호선을 LOW로 만들지 않는 한 신호는 HIGH로 유지 된다.

  

이것은 하나의 장치가 신호선을 LOW로 만든 상황에서 다른 장치가 신호선을 HIGH로 만들려고 해도 LOW로 유지되기 때문에 신호 선점을 위한 다툼이 없고 이로 인하여![[Untitled 2 7.png|Untitled 2 7.png]]

  

  

# I2C 통신의 원리

![[/Untitled 2 7.png|Untitled 2 7.png]]

> [!info] I2C 통신에 대한 깔끔한 설명 - 원리부터 응용까지 (with 온도센서)-2  
> 목차 1.  
> [https://ohj-1129.tistory.com/38](https://ohj-1129.tistory.com/38)