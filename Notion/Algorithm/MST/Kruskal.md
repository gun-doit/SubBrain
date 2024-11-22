### 탐욕적인 방법, 간선 선택 기반 방법 [[링크](https://gmlwjd9405.github.io/2018/08/29/algorithm-kruskal-mst.html)**]**

### **시간 복잡도 :** $O(elog_2e)$﻿

> 동작

1. 그래프의 간선을 오름차순으로 정렬
2. 정렬된 간선에 리스트에서 순서대로 사이클을 형성하지 않는 간선을 선택
    1. **유니온 파인드**를 통해 사이클 생성 여부 확인
3. MST에 추가.

  

```C++
struct Edge{
    int node[2];
    int distance;

    Edge(int a, int b, int distance){
        node[0] = a;
        node[1] = b;
        distance = distance;
    }

    bool operator < (const Edge& other) const{
        return distance < other.distance;
    }
};
vector<Edge> v;
int parent[6];

// union_find
namespace union_find{
    int findParent(int node){
        if(parent[node] == node) return node;
        return findParent(parent[node]);
    }

    void unionParent(int node1, int node2){
        node1 = findParent(node1);
        node2 = findParent(node2);
        if(node1 < node2) parent[node2] = node1;
        else parent[node1] = node2;
    }

    bool isCycle(int node1, int node2){
        node1 = findParent(node1);
        node2 = findParent(node2);
        if(node1 == node2) return true;
        else return false;
    }
}

void kruskal(){
    // 가중치 기준 오름차순 정렬
    sort(v.begin(), v.end());

    // 부모 노드 초기화
    for(int i = 1; i<=5; i++){
        parent[i] = i;
    }

    // 간선의 가중치 합
    int sum = 0;

    for(int i =0; i<v.size(); i++){
        // 사이클 여부 확인
        if(!isCycle(v[i].node[0], v[i].node[1])){
            sum += v[i].distance;
            unionParent(v[i].node[0], v[i].node[1]);
        }
    }

    //가중치 합 출력
    cout << sum << endl;
    return;
}
```