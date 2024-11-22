> [https://seosh817.tistory.com/345](https://seosh817.tistory.com/345)
> 
> [https://docs.docker.com/engine/install/ubuntu/](https://docs.docker.com/engine/install/ubuntu/)  
>   
> [https://velog.io/@lijahong/0부터-시작하는-Docker-공부-Docker-Image-생성하기](https://velog.io/@lijahong/0부터-시작하는-Docker-공부-Docker-Image-생성하기)
> 
> [https://www.slideshare.net/slideshow/ss-170827801/170827801](https://www.slideshare.net/slideshow/ss-170827801/170827801)
> 
> [https://velog.io/@markany/도커에-대한-어떤-것-1.-도커란-무엇인가](https://velog.io/@markany/도커에-대한-어떤-것-1.-도커란-무엇인가)
> 
> [https://squirmm.tistory.com/entry/Docker-도커란-무엇인가](https://squirmm.tistory.com/entry/Docker-도커란-무엇인가)
> 
> [https://be-developer.tistory.com/18](https://be-developer.tistory.com/18)
> 
> [https://adjh54.tistory.com/category/Docker](https://adjh54.tistory.com/category/Docker)

  

### 도커란?

**리눅스 컨테이너에 리눅스 어플리케이션을 프로세스 격리기술을 사용하여 더 쉽게 컨테이너로 실행**

**하고 관리할 수 있게 해주는 오픈소스 프로젝트**

**도커 엔진은 컨테이너를 생성하고 관리하는 주체로서 이 자체로 컨테이너를 제어할 수 있고 다양한 기능을 제공하는 도커의 프로젝트이다.**

  

### Virtual Machine (가상머신) vs Docker Container (도커 컨테이너)

![[Untitled 22.png|Untitled 22.png]]

### 가상머신

**하이퍼바이저를 이용해 여러개의 운영체제를 하나의 호스트에서 생성해서 사용하는 방식**

**⇒ 게스틑 운영체제를 사용하기 위한 라이브러리, 커널 등을 전부 포함하기 때문에 가상 머신을 배포하기 위한 이미지로 만들었을 때 이미지의 크기 또한 커진다.**

  

- **가상머신은 Hyperviesor를 통해 여러개의 운영체제를 생성하고 관리된다.**
- **시스템 자원을 가상화하고 독립된 공간을 생성하는 작업은 HyperVisor를 거치므로 → 성능 손실이 크다.**
- **Guest OS를 사용하기 위한 라이브러리, 커널 등을 포함하므로 → 배포할 때 용량이 크다**

---

### 도커

**가상화된 공간을 생성하기 위해 리눅스 자체 기능인 chroot, 네임스페이스(namespace), cgroup을 사용함으로써 프로세스 단위의 격리 환경을 만들기 때문에 성능 손실이 거의 없다. 컨테이너에 필요한 커널을 공유해서 사용하고, 컨테이너 안에는 어플리케이션을 구동하는 데 필요한 라이브러리 및 실행파일만 존재하기 때문에 컨테이너를 이미지로 만들었을 때 이미지의 용량 적다.**

  

- **가상화된 공간을 생성할 때 리눅스 자체 기능을 사용하므로 프로세스 단위 격리 환경을 만드므로 → 성능 손실 없음**
- **가상머신과 달리 커널을 공유해서 사용하므로, 컨테이너에는 라이브러리 및 실행파일만 있다. → 용량이 적다.**

**⇒ 배포하는 시간이 가상 머신에 비해 빠르며, 사용할 때의 성능 손실 또한 거의 없다.**