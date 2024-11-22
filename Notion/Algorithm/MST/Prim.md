### 시작 정점에서 출발하여 신장트리 집합을 확장해나가는 방법, 정점 선택 기반

### 시간 복잡도 : $O(n^2)$﻿ or $O(ElogV)$﻿ [V+E 지만 [E > V] 이기 때문에] [[링크](https://www.weeklyps.com/entry/%ED%94%84%EB%A6%BC-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-Prims-algorithm)]

> **동작**

1. 임의의 정점을 선택하여 비어있는 T에 포함시킨다. ( T는 노드가 한개인 트리 )
2. T에 있는 노드와 T에 없는 노드 사이의 간선 중 가중치가 최소인 간선을 찾는다
3. 찾은 간선이 연결하는 두 노드 중, T에 없던 노드를 T에 포함시킨다.
4. 모든 노드가 T에 포함될 때 까지, 1,2,를 반복

  

### $O(V^2)$﻿

```C++
vector<pair<int,int>> ad[N] // ad[i] : i 노드가 출발지인 간선들, first = 목적지, second= 비용
int dist[N]; // dist[i] : 선택된 노드들과 i 노드가 연결되어 있는 간선의 비용 중 최소 비용
bool selected[N]; // selected[i] : i가 이전에 선택된 노드인가?

long long prim(int pn){
    long long ret = 0;
    for(int i = 1; i<=pn; i++){ //초기화
        dist[i] = INF;
        selected[pn] = false;
    }
    dist[1] = 0;    // 1번 노드 선택
    for(int i = 1; i<=pn; i++){
        int now = -1, min_dist = INF;
        for(int j = 1; j<=pn; j++){
            if(!selectedj[j] && min_dist > dist[j]){
                min_dist = dist[j];
                now = j;
            }
        }

        if(now < 0 ) return (long long)INF; //연결 그래프가 아님
        
        ret += min_dist;
        selected[now] = true;
        for(auto edge : ad[now]){
            dist[edge.first] = min(dist[edge.first], edge.second);
        }
    }
    return ret;
}                
```

  

### $O(ElogV)$﻿

```C++
void Prim(int start){
    visited[start] = 1;

    priority_queue<Edge> pq;

    for(int i = 0; i<v[start].size(); i++){
        int next = v[start][i].node;
        int nextCost = v[start][i].distance;

        pq.push({next, nextCost});
    }

    while(!pq.empty()){
        int now = pq.top().node;
        int nowCost = pq.top().distance;
        pq.pop();

        if(visited[now] == 1){
            continue;
        }

        visited[now] = 1;

        ans += nowCost;

        for(int i = 0; i<v[now].size(); i++){
            int next = v[now][i].node;
            int nextCost = v[now][i].distance;

            pq.push({next, nextCost});
        }
    }

}
```

차이점

1. 프림은 다익스트라와 달리 두 노드 사이의 최단거리가 아닐 수 있다.