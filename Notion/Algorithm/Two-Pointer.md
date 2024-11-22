  

> **리스트에 순차적으로 접근해야 할 때 두 개의 점 위치를 기록하면서 처리하는 알고리즘  
> 정렬되어있는 두 리스트의 합집합에도 사용됨. 병합정렬의 counquer 영역의 기초가 되기도한다.ㅈ  
> **

**시간복잡도 : O(N)**

```C++
int start = 0, end = 0; 
```

  

  

### 동작 방식

1. 두 개의 포인트를 만든다.
2. start ≤ end의 조건을 가진다.

---

1) [투 포인터 알고리즘](https://velog.io/@heyggun/Algorithm-Two-Pointers-Algorithm-%ED%88%AC-%ED%8F%AC%EC%9D%B8%ED%84%B0-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98)