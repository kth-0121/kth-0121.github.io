---
title: Bidirectional Dijkstra's Algorithm
date: 2026-06-23 15:00:00 +0900
categories: [Algorithm, Graph]
tags: [algorithm, dijkstra, shortest-path]
toc: true
comments: true
---

# Bidirectional Dijkstra's Algorithm

## Introduction

다익스트라(Dijkstra) 알고리즘은 하나의 시작 정점에서 모든 정점까지의 최단 거리를 구하는 대표적인 알고리즘이다.

하지만 **특정 시작점(Source)과 도착점(Target) 사이의 최단 경로만 필요하다면**, 시작점에서만 탐색하는 것은 비효율적일 수 있다.

**Bidirectional Dijkstra**는 시작점과 도착점에서 동시에 탐색을 진행하여 두 탐색이 중간에서 만나는 지점을 찾는 방식이다.

이 방법은 탐색해야 하는 정점의 수를 줄일 수 있어 대규모 그래프에서 일반적인 Dijkstra보다 더 빠르게 동작하는 경우가 많다.



## Time Complexity

일반적인 Dijkstra 알고리즘의 시간 복잡도는 다음과 같다.

$$
O((V + E)\log V)
$$

Bidirectional Dijkstra 역시 이론적인 최악 시간 복잡도는 동일하다.

$$
O((V + E)\log V)
$$

하지만 실제로는 양쪽에서 탐색을 수행하기 때문에 방문하는 정점 수가 크게 감소하여 평균 실행 시간이 더 빠른 경우가 많다.



## Simple Example

아래는 Bidirectional Dijkstra을 C++을 사용하여 구현한 예제이다.

```cpp
#include <bits/stdc++.h>

using namespace std;

#define INF LLONG_MAX

struct Edge
{
    int to;
    long long weight;
};

void addEdge(
    vector<vector<Edge>>&g,
    vector<vector<Edge>>&rg,
    int from,int to,long long weight)
{
    g[from].push_back({to,weight});
    rg[to].push_back({from,weight});
}

long long bidirectionalDijkstra(
    int n,
    vector<vector<Edge>>&g,
    vector<vector<Edge>>&rg,
    int s,int t)
{
    if(s==t) return 0;
    
    vector<long long> 
}
                                
int main()
{
    int n,e,from,to,s,t;long long weight;
    cin >> n >> e;
    vector<vector<Edge>> g(n);
    vector<vector<Edge>> rg(n);
    for(int i=0;i<e;i++){
        cin >> from >> to >> weight;
        addEdge(g,rg,from,to,weight);
    }
    cin >> s >> t;
    cout << "Shortest Distance: "
         << bidirectionalDijkstra(n,g,rg,s,t);
    return 0;
}
```

