> **Serial Peripheral Interface : 직렬 주변 기기 인터페이스**

**2C, CAN, UART와 같은 시리얼 통신 방식 중 한 가지로 마이크로컨트롤러, 시프트 레지스터, SD 카드 등의 소형 주변 장치 사이에 데이터를 전송하기 위한 기능이다.**

  

### 특징

**1 : N의 통신 방식을 지원하는 동기식 통신 방식이라는 것이다. 다만 다수의 통신을 위해서는 다수만큼 선이 필요하다는 단점이 있다. 또한 동시에 송수신이 가능하며** **$I^2C$**﻿**에 비해 속도가 빠르다. 또한 단순 센서, 메모리와 같은 칩과 칩 사이의 통신에 많이 사용하기도 한다.**

**SPI 통신은 하나의 마스터 기기와 하나 이상의 스레이브 기기를 연결하여 사용한다.**

![[Untitled 9.png|Untitled 9.png]]

- `**SCLK(SCK)**` **: 동기화 신호임며 클럭 전송을 위한 단자로, 마스터에서 슬레이브로 클럭을 전송한다.**
- `**MOSI**` **: Master Output Slave Input, 마스터에서 슬레이브로 데이터를 전송한다.**
- **`MISO`** **: Master Input Slave Output, 슬레이브에서 마스터로 데이터를 전송한다.**
- `**CS(=SS)**` **: Chip Select, 보통 SS핀 즉 Slave Select로 슬레이브를 선택할 때 사용된다. 마스터에서 슬레이브 장치를 선택하기 위한 단자이다.**

  

### Shift Resgister

**기본적으로 MSB부터 전송되는데 특정 컨트롤러는 LSB부터 전송을 수행시키는 방법도 지원한다. 아래 그림처럼 SHIFT REGISTER에 의해서 데이터가 이동한다.**

![[Untitled 1 2.png|Untitled 1 2.png]]

마스터에서 슬레이브로 값을 보낸다고 가정했을 때, 1 Clock 신호마다 1bit의 data가 이1동한다

![[Untitled 2 2.png|Untitled 2 2.png]]

  

### 1 : N 형태의 SPI

![[Untitled 3 2.png|Untitled 3 2.png]]

  

  

### 장점

1. 완전한 전이중 통신 : 양방향 통신이다. 즉, 동시에 송수신이 가능하다.
2. 전송되는 비트에 대한 완전한 프로토콜 유연성 : 최대 16비트까지 맘대로 길이를 조절할 수 있다.
3. 전송기가 필요하지 않다 : 트랜시버를 사용할 필요가 없다.
4. 매우 단순한 하드웨어 인터페이스 처리
5. IC 패키지에 4개의 핀만 사용
6. 최대 클럭이 제한되지 않아 속도 제한이 없다.
7. Push-Pull 출력(Open Drain이 아닌)을 사용하여 상호 간의 같은 전압을 사용하여 시그널 정합성과 고속을 지원한다.
8. $I^2C$﻿ 보다 낮은 소비 전력

  

### 단점

1. 하드웨어 슬레이브 인식이 없음.
2. 슬레이브에 의한 하드웨어 흐름 제어가 없다.
3. 오류 검사 프로토콜이 정의되어 있지 않음
4. RS232, CAN버스보다 비교적 더 짧은 거리에서 동작.
5. 하나만의 마스터 장치만 지원.
6. 인밴드를 통해 주소가 지원되지 않아 다 수의 슬레이브를 사용 시 별도의 아웃밴드를 통해 슬레이브를 선택해야 한다.

  

  

---

1. [SPI 통신이란](https://aliencoder.tistory.com/92)
2. [SPI 통신에 대하여](https://blog.naver.com/emperonics/221714005614)
3. [SPI란](https://velog.io/@lutein/SPISerial-Peripheral-Interface%EB%9E%80)
4. [[시리얼 통신] SPI(Serial Peripheral Interface)통신이란? — 외부 저장소 (tistory.com)](https://aliencoder.tistory.com/92)
5. [SPI(Serial Peripheral Interface)란? (velog.io)](https://velog.io/@lutein/SPISerial-Peripheral-Interface%EB%9E%80)