> **Internet Protocol : 송신 호스트와 수신 호스트가 패킷 교환 네트워크에서 정보를 주고받는 데 사용하는 정보의 규약**

> **인터넷에서 데이터 주소를 지정하고 라우팅하기 위한** ==**요구 사항의 집합.**== **여러 전송 프로토과 함께 사용할 수 있다.**![[Untitled 39.png|Untitled 39.png]]ng]]

  

ver : IPv4, IPv6 주소체계 중 어떤 버전을 사용하고 있는지 나타낸다.

head length : 헤더의 길이(bytes), 데이터 한 줄이 32bits( 4bytes ) 라고 적혀 있으므로 5줄 * 4 bytes 총 20 bytes가IP의 기본적인 헤더 길이

type of service : IP 데이터의 타입을 표시, 거의 사용X, 미 국방부에서 만들어즴.

length : 전체 데이터의 길이

16-bit identifier, flags, fragment offset : 단편화, 재결화를 위해 사용한다.

time to live : TTL 데이터가 건너갈 수 있는 남아있는 hop 수를 표시 ( 라우터 하나를 건너가는 것을 한 hop 이라고 한다.

upper layer : IP위에 존재하는 전송 계층의 프로토콜을 표시( TCP or UDP) 혹은 ICMP 프로토콜이 될 수도 있다.

header checkshum : 받은 데이터에 에러가 있는지 없는지 에러 검출을 하기 위해 사용한다. TCP의 경우 신뢰성있는 데이터 전송을 위해 비트라도 에러가 있으면 재전송, UDP도 checksum 계산을 하지만 오류를 정정해주진 않는다. 필드명이 header checksum인 이유는 전송 계층에서 내려온 데이터는 checksum 계산을 하지 않고 header에 대해서만 에러 검출 동작을 하기 때문에.

source, dest IP address : **출발지와 목적지 IP , 32bits인 이유는 IPv4를 사용하기 때문이다.**

options : 추가적인 정보를 기록한다. ex) 특정 라우터를 지나간 timestamp 등이 필요하다면 옵션에 추가, 기본적으로 20bytes

data : 전송 계층에서 내려온 데이터(payload)

  

  

## IP 단편화 및 재결합

MTU ( Maximum Transmission Unit ) 사이즈 → 데이터의 최대 크기가 존재하며 MTU 사이즈는 네트워크 링크의 종류에 따라 다르다. ex) Wifi와 Ethernet은 MTU사이즈가 다르며 Etherent은 MTU 사이즈가 1500bytes로 정해져 있다.

단편화 ( Fragmentation ) → 큰 MTU 사이즈를 가진 네트워크에서 작은 MTU 사이즈를 가진 네트워크로 데이터를 이동시켜야 한다면, 데이터를 쪼개야 한다.

재결합 ( reassembly ) → IP header에는 쪼개진 datagram 조각의 순서를 식별하기 위한 필드가 포함되어 있다. 쪼개진 datagram을 마지막 도착지에서 쪼개진 데이터를 다시 합치는 것.

  

  

## IPv4 주소체계

> **32bit로 구성되어 있으며 한 칸당 10진 8bit IP주소로 구성되어 있다.**

호스트 or 라우터 네트워크 인터페이스마다 하나씩 존재한다. 하지만, 라우터 혹은 호스트의 대부분은 두 개 이상의 네트워크 인터페이스가 존재하므로 IP주소로 여러개 존재할 수 있다.

  

### 서브넷 (subnets)

> IP 주소에서 동일한 장치의 인터페이스를 말한다. 서브넷 안에서는 라우터 없이 연결되어 이ㅣㅆ다.

1. 서브넷을 나타내는 부분 - 상위 bits
2. 네트워크 안에서의 호스트를 나타내는 부분 - 하위 bits

  

서브넷 마스크 - 상위 몇 비트까지 서브넷을 사용할 것인가를 나타내며 /로 나타낸다.

CIDR ( Classless Inter-Domain Routing ) - IETF에서 93년부터 도입한 표준 IP 주소 할당 방식으로 8, 16, 24비트가 아닌 23비트 15비트 등으로 서브넷을 구분한다

⇒ 고갈되는 IP주소를 기존의 클래스 기반 IP 주소 할당 방식보다 더 효율적으로 사용할 수 있는 장점이 있다.

DHCP ( Dynamic Host Configuration Protocol ) - 동적으로 IP주소를 할당 받는 ![[Untitled 1 14.png|Untitled 1 14.png]]가능

→ 네트워크에 접속하고자 하는 이동 사용자 지원

![[/Untitled 1 14.png|Untitled 1 14.png]]

  

### NAT (![[Untitled 2 6.png|Untitled 2 6.png]] 등의 장비에서 다수의 사설 IP를 외부IP로 네트워크 주소를 변환하는 기술

![[/Untitled 2 6.png|Untitled 2 6.png]]

장점

1. 모든 라우터에 물려있는 장비에 대해서 하나의 주소만 ISP를 받아오면 된다.
2. 외부 IP와 내부 IP가 독립적으로 설정되어 있으므로 내부 주소를 변경하더라도 외부에는 영향이 없다.
3. 2번과 마찬가지로 독립적으로 외부 ISP를 변경하더라도 내부에는 영향이 없다.
4. 내부 네트워크 주소가 외부에 노출되지 않으므로 보안의 측면에서 장점이 있다.

  

## IPv6 주소체계

> 128-bits로 구성되어 있으며 한 칸당 16-bit를 4자리의 16진수로 표현하며 8조각으로 구성된 IP 주소로 구성되어 있습니다.
![[Untitled 3 4.png|Untitled 3 4.png]]der 형식 개선으로 우선순위 및 품질에 따라 순차적 할당 기능 등의 QoS 지원
3. 보안 기능을 기본적으로 지원

![[/Untitled 3 4.png|Untitled 3 4.png]]

  

ver → IPv4 주소체계, IPv6 주소체계 중 어떤 버젼을 사용하고 있는지.

pri (트래픽 클래스 ) → QoS용 필드며 기본 값은 0

flow label - 같은 ‘flow’에 속한 데이터를 구별하기 위해 사용되는 필드

payload len - 원본 데이터의 길이

next header → IPv4는 upper layer였지만 IPc6는 next header를 정의

hop limit → IPv4의 TTL 필드 명청이 바뀐 것, 중계 가능한 라우터 수를 나타내고 중계할 때마다 줄어든다

sourcer, dest IP address → 출발지와 목적지 IP주소

  

터널링 ( turnnelling ) → IPv4 라우터에서 IPv4의 datagram의 payload에 IPv6의 datagram을 넣어서 전달함으로써 IPv6와의 호환성을 ㄹ해결한다.

---

1) [**개발은 재밌어야한다.**](https://dreamcoding.tistory.com/33)

2) [IP프로토콜 개념 정리](https://seosh817.tistory.com/33)