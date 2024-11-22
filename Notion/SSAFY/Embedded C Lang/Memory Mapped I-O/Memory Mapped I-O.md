### Memory Map이란

- **메모리와 I/O device에 고유한 address를 부여하는 것이다.**
- **메모리를 어떻게 분배하고 사용할 것인지를 결정하는 것이다.**
- **모든 컴퓨터는 memory map을 가지고 있고, 프로그래머는 memory map에 따라 address를 사용한다.**

  

  

### Memory Mapped I/O

> **메모리 지도에 실제 메모리가 맵핑 되어있는 것**

![[Untitled 35.png|Untitled 35.png]]

**⇒ 맵핑 되지 않은 빈 공간은** ==**Reserved**==

⇒ 메모리 맵을 보면서 개발을 한다, → 이러한 제어 방식을 Memory Mapped I/O라고 한다.

---

1. [Microcontroller, Memory Map, Processor Databook (tistory.com)](https://gofo-coding.tistory.com/entry/Microcontroller-Memory-Map-Processor-Databook#:~:text=Memory%20map%EC%9D%B4%EB%9E%80%2C%20%EB%A9%94%EB%AA%A8%EB%A6%AC%EC%99%80%20I%2FO%20device%EC%97%90%20%EA%B3%A0%EC%9C%A0%ED%95%9C%20address%EB%A5%BC%20%EB%B6%80%EC%97%AC%ED%95%98%EB%8A%94,%EA%B0%80%EC%A7%80%EA%B3%A0%20%EC%9E%88%EA%B3%A0%2C%20%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%A8%B8%EB%8A%94%20memory%20map%EC%97%90%20%EB%94%B0%EB%9D%BC%20address%EB%A5%BC%20%EC%82%AC%EC%9A%A9%ED%95%9C%EB%8B%A4.)