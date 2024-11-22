> **가중치가 음수일때도 가능**

### 시간복잡도 : $O(VE)$﻿

**동작**

1. **출발 노드를 설정**
2. **최단 거리 테이블 초기화**
3. **다음의 과정을 (V(==정점) - 1 ) 번 반복한다.**
    1. 모든 간선 E개를 하나씩 확인한다.
    2. 각 간선을 거쳐 다른 노드로 가는 비용을 계산하여 최단 거리 테이블을 갱신한다.
4. **만약 음수 간선 순환이 발생하는지 체크하고 싶다면 3번 과정을 한 번 더 수행한다.**

  

  

```C++
void bellmanFord(){
	//최단 거리 테이블 초기화
	int dist[N] = { INF };
	
	//출발 노드 설정
	dist[s] = 0;
	
	//N-1번 반복
	for(int i = 0; i < N-1; ++i){
		//매번 모든 간선을 확인한다.
		for(int j = 0; j < E; ++j){
			int from = edges[j].first;
			int to = edges[j].second.first;
			int cost = edges[j].second.second;
			
			//한번이라도 계산된 정점에 대해서만
			if(dist[from] == INF) continue;
			
			if(dist[to] > dist[from] + cost){
				dist[to] = dist[from] + cost;
				
				//n번째에도 최단 거리가 갱신된다면 음수 싸이클이 존재
				if(i == N-2) return true;
			}
		}
	}
	return false;
}
```