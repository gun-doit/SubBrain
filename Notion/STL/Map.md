> [레드블랙트리](https://zeddios.tistory.com/237)**로 구현**

  

### Defind in header

```C++
tempate<
		class Key,
		class T,
		class compare = std::less<Key>
		class Alocator = std::allocator<std::pair<const Key,T>>
> class map;


// since c++17
namespace pmr{
		tempate<
				class Key,
				class T,
				class Compare = std::less<Key>
		> using map = std::map<Key, T, Compare, std::pmr::polymorphic_allocator<std::pair<const Key, T>>>;
}
```

  

map은 고유한 키가 있는 키-값 쌍을 포함하는 정렬된 연관 컨테이너이다. 키는 비교 기능을 사용하여 정렬된다.  
반복자는 키의 오름차순으로 반복된다.  

  

### Additional

1. **메모리 할당기의 사용**:
    - `**std::map**`은 기본적으로 `**std::allocator**`를 사용하여 메모리를 할당하고 해제합니다.
    - `**pmr::map**`은 표준 라이브러리의 메모리 리소스 관리자(PMR)를 사용하여 메모리 할당 및 해제를 처리합니다. 이를 통해 메모리 할당 및 해제에 대한 최적화와 유연성을 제공합니다. 예를 들어, 다른 종류의 메모리 할당기를 사용하여 동적 메모리 할당을 최적화할 수 있습니다.
2. **디폴트로 사용되는 비교 함수의 형태**:
    - `**std::map**`에서는 `**std::less**`를 기본적으로 사용하여 키를 비교하고 정렬합니다.
    - `**pmr::map**`에서는 사용자가 지정하지 않으면 `**std::less**`를 사용하여 키를 비교하고 정렬합니다. 그러나 PMR의 `**map**`에서는 사용자 정의 비교 함수를 제공하지 않을 수도 있습니다.