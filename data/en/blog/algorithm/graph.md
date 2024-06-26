---
title: '[알고리즘] 그래프'
date: '2021-05-05'
tags: ['algorithm']
draft: false
summary: 'A guide to using the srcset and sizes attributes to create responsive images'
images: ['/static/images/responsive-image.jpg']
authors: ['default']
---

### 1. 그래프 (Graph) 란?

- 그래프는 실제 세계의 현상이나 사물을 정점(Vertex) 또는 노드(Node) 와 간선(Edge)로 표현하기 위해 사용

### 예제 집에서 회사로 가는 경로를 그래프로 표현한 예

<img src="https://www.fun-coding.org/00_Images/graph.png" width="400"/>

### 2. 그래프 (Graph) 관련 용어

- 노드 (Node): 위치를 말함, 정점(Vertex)라고도 함
- 간선 (Edge): 위치 간의 관계를 표시한 선으로 노드를 연결한 선이라고 보면 됨 (link 또는 branch 라고도 함)
- 인접 정점 (Adjacent Vertex) : 간선으로 직접 연결된 정점(또는 노드)

- 참고 용어
  - 정점의 차수 (Degree): 무방향 그래프에서 하나의 정점에 인접한 정점의 수
  - 진입 차수 (In-Degree): 방향 그래프에서 외부에서 오는 간선의 수
  - 진출 차수 (Out-Degree): 방향 그래프에서 외부로 향하는 간선의 수
  - 경로 길이 (Path Length): 경로를 구성하기 위해 사용된 간선의 수
  - 단순 경로 (Simple Path): 처음 정점과 끝 정점을 제외하고 중복된 정점이 없는 경로
  - 사이클 (Cycle): 단순 경로의 시작 정점과 종료 정점이 동일한 경우

단순 경로 (A - B - C)

<img src="https://www.fun-coding.org/00_Images/simplepath.png" width="200"/>

## 3. 그래프 (Graph) 종류

### 무방향 그래프 (Undirected Graph)

- 방향이 없는 그래프
- 간선을 통해, 노드는 양방향으로 갈 수 있음
- 보통 노드 A, B가 연결되어 있을 경우, (A, B) 또는 (B, A) 로 표기

<img src="https://www.fun-coding.org/00_Images/undirectedgraph.png" width="300"/>  

### 연결 그래프 (Connected Graph) 와 비연결 그래프 (Disconnected Graph)

- 연결 그래프 (Connected Graph)
  - 무방향 그래프에 있는 모든 노드에 대해 항상 경로가 존재하는 경우
- 비연결 그래프 (Disconnected Graph)
  - 무방향 그래프에서 특정 노드에 대해 경로가 존재하지 않는 경우

비연결 그래프 예

<img src="https://www.fun-coding.org/00_Images/disconnectedgraph.png" width="300"/>  

### 사이클 (Cycle) 과 비순환 그래프 (Acyclic Graph)

- 사이클 (Cycle)
  - 단순 경로의 시작 노드와 종료 노드가 동일한 경우
- 비순환 그래프 (Acyclic Graph)
  - 사이클이 없는 그래프

비순환 그래프 예

<img src="https://www.fun-coding.org/00_Images/acyclicgraph.png" width="300"/>  

### 완전 그래프 (Complete Graph)

- 그래프의 모든 노드가 서로 연결되어 있는 그래프

완전 그래프 예

<img src="https://www.fun-coding.org/00_Images/completegraph.png" width="300"/>  

- 트리는 그래프 중에 속한 특별한 종류라고 볼 수 있음

### 3. 그래프와 트리의 차이

<table>
  <tr>
    <th></th>
    <th>그래프</th>
    <th>트리</th>
  </tr>
  <tr>
    <td>정의</td>
    <td>노드와 노드를 연결하는 간선으로 표현되는 자료 구조</td>
    <td>그래프의 한 종류, 방향성이 있는 비순환 그래프</td>
  </tr>
  <tr>
    <td>방향성</td>
    <td>방향 그래프, 무방향 그래프 둘다 존재함</td>
    <td>방향 그래프만 존재함</td>
  </tr>
  <tr>
    <td>사이클</td>
    <td>사이클 가능함, 순환 및 비순환 그래프 모두 존재함</td>
    <td>비순환 그래프로 사이클이 존재하지 않음</td>
  </tr>
  <tr>
    <td >루트 노드</td>
    <td>루트 노드 존재하지 않음</td>
    <td>루트 노드 존재함</td>
  </tr>
  <tr>
    <td>부모/자식 관계</td>
    <td>부모 자식 개념이 존재하지 않음</td>
    <td>부모 자식 관계가 존재함</td>
  </tr>
</table>
