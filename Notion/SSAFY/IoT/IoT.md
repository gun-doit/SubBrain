> **Internet of Things : 모든 사물이 인터넷에 연결되어 관리되는 것.**

  

# 1DAY

사물 인터넷 구성 방식

- 사물인터넷의 네트워크 및 장비의 구성 방식에 대해 학습한다.
- 프로젝트를 구성할 때 어떤 방식으로 장치를 연결하고 데이터를 처리할 지 학습한다.

  

  

  

### IoT 구성도

- **Main Server : 서비스의 모든 Data를 관리하는 server**
- ==**GateWay**== **: Edge 로부터 먼저 Data를 받고, Main server로 보내주는 중간 관리자**
- **Edge : 최말단 기기**

**⇒ Main Server와 Edge가 1:1로 직접적으로 연결되면,** ==**Edge의 응답에 Main Server가 계속 대기 하게 되어 효율이 감소**==**한다.**

**⇒ Edge는 잦은 고장, 인터넷이 연결되지 않는 환경에 노출 될 수 있다.**

  

### ESP32

> **Wifi + Bluetooth가 내장된 MCU 보드**
> 
> **Arduino 호환이라는 메리트가 있음**

![[Untitled 15.png|Untitled 15.png]]

# SSAFY PJT

> **개발 환경**
> 
> **ESP32 : 아두이노 개발 환경으로 개발 가능한 IoT보드**
> 
> **라즈베리파이 : 여러 대의 ESP32를 제어하는 중간 관리자 역할을 할 보드**
> 
> **Node-RED : IBM에서 만든 IoT 프로그램**
> 
> **AWS-IoT : AWS에서 제공하는 IoT 서비스**
> 
> **Firebase : Google에서 제공하는 백엔드 플랫폼, DB Server용도로 사용**
> 
> **ThingSpeak : IoT GUI 화면을 구성해주는 웹 서비스**

![[Untitled 1 7.png|Untitled 1 7.png]]

  

  

  

  

  

---

1. [아두이노 ESP32 배터리 소모량 과 성능비교 : 네이버 블로그 (naver.com)](https://blog.naver.com/PostView.naver?blogId=elpina75&logNo=221626120127)