[링크](https://velog.io/@chosj1526/%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EC%9C%A0%EB%8B%88%EC%98%A8-%ED%8C%8C%EC%9D%B8%EB%93%9C#-%EC%B5%9C%EC%A0%81%ED%99%94%ED%95%98%EA%B8%B0)

**Disjoint Set - 서로서 집합**

  

## 핵심 이론

### Union 연산

- 각 노드가 속한 집합을 하나로 합치는 연산
- 노드 a, b가 a∈A, b∈B 일 때, union(a,b)는 AUB를 말한다.

### Find 연산

- 특정 노드 a에 관해 a가 속한 집합의 대표 노드를 반환하는 연산
- 노드 a가 a∈A일 때, find(a)는 A 집합의 대표 노드를 반환한다  
    ⇒해당 원소들의 parent를 비교하고 연결의 참/거짓을 확인한다.