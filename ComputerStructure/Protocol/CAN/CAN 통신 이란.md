# CAN 통신이란
차랑 내에서 호스트 컴퓨터 없이 마이크로 컨트롤러나 장치들이 서로 통신하기 위한 표준 통신 규격이다.
![[Pasted image 20241218095728.png]]

# 통신 회로 구성
![[Pasted image 20241218110515.png]]
제어기 내의 CAN 통신 회로 구성은 위의 블럭도와 같다. CAN BUS로 CAN_H와 CAN_L 신호를 주고 받으며, CAN BUS는 제어기 커넥터를 통해 연결된 후 CAN 트랜시버로 연결된다.


CAN H와 CAN L의 파형은 아래 그림의 오른쪽과 같습니다. CAN H는 2.5V~3.5V 전압을, CAN L는 2.5V~1.5V 전압을 사용합니다. 
CAN H와 CAN L의 전위차가 없을 때는 recessive (열성), 
CAN H와 CAN L의 전위차가 있을 때는 dominant (우성)
즉, CAN 통신은 두 라인의 전위차를 통해 데이터를 전달한다.

![[Pasted image 20241218110701.png]]
1. CAN 트랜시버가 CAN BUS의 CAN_H, CAN_L 신호를 통해 Recessive인지 Dominant인지 판단한다. 그리고 CAN 트랜시버의 RX를 통해 Recessive면 HIGH, Dominant면 LOW 신호를 MCU에게 전달한다.
2. MCU에서 CAN BUS로 데이터를 전송할 때는 MCU의 LOW신호와 HIGH신호를 CAN 트랜시버가 CAN_H, CAN_L 신호 형태에 맞게 변환해 준다.
![[Pasted image 20241218110951.png]]

# CAN 트랜시버 내부 회로도
![[Pasted image 20241218111007.png]]
위의 CAN 트랜시버 회로와 같이 MCU의 TX에서 HIGH신호를 보내면 FET는 비활성화되어 2.5V 풀업저항에 의해 CAN_H, CAN_L가 모두 2.5가 된다. 반대로 MCU에서 TX에서 LOW신호를 보내면 FET는 활성화되어 CAN_H 5V, CAN_L는 GND 전위가 된다.


--- 
[CAN 통신의 개요 (Controller Area Network) : 네이버 블로그](https://m.blog.naver.com/lagrange0115/221941482740)
