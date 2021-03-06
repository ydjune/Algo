# MST (minimun spanning tree)
  
spanning tree : spen(덮다)라는 말 처럼, 모든 정점을 포함하는 트리를 말함.  
그 중에 최소(V-1개 edge를 가짐)를 찾는 것.  
같은 비용인 2개 이상의 MST를 가질 수 있음.  
  
## 크루스칼 알고리즘
E개 간선을 가중치가 감소하지 않는 순서로 정렬.  
각 간선을 Greedy하게 MST에 추가.  
(사이클 검사는 유니온 파인트로 쉽게 가능)  
전체 수행 시간 : O(정렬+각 간선 추가 시도*유니온파인드) -> O(ElgV)  
  
  
```c++
sort(EdgeList.begin(), EdgeList.end()); // 간선의 가중치에 따라 정렬

int mst_cost = 0;
UnionFind UF(V);  // 각 정점이 여러개 그룹
for(int i = 0; i < E; ++i){
    pair<int, ii> front = EdgeList[i];  // 정렬된 edge를 하나 가져와서
    if (!UF.isSameSet(u, v)){ // u, v 정점이 같은 그룹인지 검사
        mst_cost += asd;  // 서로 다른 그룹이면 둘사이 (u,v)간선의 가중치 더함
        UF.unionSet();    // 추가된 간선을 연결하고 하나의 그룹으로 만듬
    }
}
```
위 코드는 마지막 간선까지 검사하지만 보통 그 전에 끝낼 수 있다.  
예를 들어 정점 모두 방문하면 끝난다던지...  

## 프림 알고리즘
하나의 정점을 선택해서 선택하지 않은 정점으로 가면서 MST를 구함.  
우선순위 큐에 가중치가 증가하는 순서로 정렬되고, 거기서 하나씩 꺼내서 연결(정점이 선택되지 않은것 == 사이클이 아닐때).  
전체 수행 시간 : O(각 간선을 한번씩 처리 * 우선순위 큐 삽입,삭제 비용) -> O(ElgV)  
  
```c++
priority_queue q; // STL 기본은 최대 힙
void process(int vtx){
    taken[vtx] = 1; // 정점 선택 표시
    for(int j = 0; j < adj[vtx].size(); ++j){ // vtx와 연결된 정점
        int v = adj[vtx][j];
        if (!taken(v))  // 방문하지 않으면
            q.push(v);
    }
}
void main(){
    process(0); // 시작정점 0을 선택하고 모든 간선 처리
    mst_cost = 0;
    while(!q.empty()){
        (u,v,w) = q.top(); q.pop(); // u(시작정점), 추가할 정점 v, 가중치 w
        if (!taken[v]){
            mst_cost += w;
            process(v);
        }
    }
}
```

## 몇 가지 활용 예
### '최대' 스패닝 트리
### '최소' 스패닝 서브 그래프
### 최소 '스패닝 포레스트'
### 두 번째 스패닝 트리
### 미니맥스, 맥시민
