> **Protocal : 통신 규약 및 약속**

  

IoT 인터페이스는 무선 단말의 특성상 ==저전력==, ==경량화된 프로토콜==이 요구된다.

(==센서 네트워크와== 마찬가지의 특징)

  

대표적으로 두 가지 프로토콜이 후보로 꼽힌다.

  

### MQTT ( Message Queue Telemetry transport)

==TCP기반==의 경량화된 Publish-Subscribe 메시지 프로토콜이다. Publish-Subscribe는 SW아키텍처 스타일에서 등장하는 모델과 동일한 내용입니다. 출판/구독 아키텍처에서 특정 이벤트를 발생시킨는 “출판자”와 해당 이벤트를 구독하는 “구독자”처럼 MQTT프로토콜에서는 브로커(Broker) 서버가 “토픽”이라고 부르는 이벤트 발생자와 구독자를 다대다(N:M)로 중개하는 메시지 버스 역할을 합니다.

  

토픽 : 계층형 자료구조로 마치 디렉토리를 표기하는 것처 처럼 /(슬래시)를 기준으로 계층적으로 데이터를 표현합니다. 이 토픽은 MQTT Broker를 통해 구독자인 다수의 클라이언트로 전달됩니다.

  

MQTT의 또 다른 특징은 QoS를 지원한다는 점이다. 서비스 종류에 따라 총 3단계의 QoS를 지원하고 있습니다.

### CoAP ( Constrained Application Protocal )

저전력 비동기 통신 프로토콜이다. MQTT와 다르게 UDP를 기반으로 비동기 통신을 사용합니다. 당연히 더 가볍고 부하가 적다. 대신 TCP와 다르게 전송 여부 신뢰성을 확인할 수 없으므로 Confirmation/Non-Confirmation message, Rest Message 같은 메시지를 통해 보완을 하고 있다.

  

프로토콜 경량화를 위해 UDP를 사용하는 것 뿐만 아니라 프로토콜 레이아웃도 단순화 하여 전문의 Header는 Binary 형태로 사이즈를 줄였다.

  

추가적인 특징으로 RESTful 방식을 지원하여, 암호화를 위해 DTLS(Datagram Transport Layer Security)을 사용한다. (TCP 기반이 아니므로 SSL/TLS는 사용 불가)

MQTT와 다르게 1:1 프로토콜이며 Pub/Sub 메시지큐 기능을 사용하지 못한다.

또한 응용프로그램 수준에서 QoS를 구현해야 하며 요청 혹은 응답 메시지에 confrimable이나 nonconfirmable을 표기해서 전송하는데 confirmable 표기된 메시지를 받는 경우 Acknowledge 응답을 해야 한다.

||MQTT|CoAP|
|---|---|---|
|기반|TCP|UDP|
|통신 노드|N : M|1 : 1|
|QoS|지원|별도 구현|
|암호화|TCP 기반 SSL사용|DTLS 사용|
|기타|Pub/Sub 모델,  <br>브로커 존재|RESTful 지원  <br>NAT 환경에서 작동 보장 못함|

  

### XMPP( eXtensible Messaging and Presence Prtocal )

XML기반의 TCP 프로토콜 이다. IETF 표준 규격으로 보통 인스턴트 메신저(Instant Messenger)를 위한 프로토콜로 많이 사용되었다. (대표적으로 구글톡에서 재버라는 이름으로 XMPP프로토콜을 사용)

각각의 노드가 마치 이메일 주소와 같이 표현되며 누구든지 분산화된 XMPP 서버를 운영할 수 있으며, 별도의 QoS를 지원하지 않는다.

  

  

---

1. [**Iot 프로토콜의 종류**](https://www.google.com/search?q=iot+%ED%94%84%EB%A1%9C%ED%86%A0%EC%BD%9C+%EC%A2%85%EB%A5%98&oq=iot+%ED%94%84%EB%A1%9C%ED%86%A0%EC%BD%9C&gs_lcrp=EgZjaHJvbWUqBwgBEAAYgAQyBggAEEUYOzIHCAEQABiABDIICAIQABgIGB4yCAgDEAAYCBgeMgYIBBBFGDzSAQk1NTY3OWowajeoAgCwAgA&sourceid=chrome&ie=UTF-8)

  

[[Protocal]]