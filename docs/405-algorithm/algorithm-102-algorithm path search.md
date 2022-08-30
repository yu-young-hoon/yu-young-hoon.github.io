---
layout: default
title: algorithm path search
parent: algorithm
nav_order: 405102
---

### BFS
* breadth first search 너비탐색
```cpp
 int n; // 입력되는 정점의 최댓값
int rear, front; // 전단과 후단을 나타내는 변수
int map[30][30], queue[30], visit[30]; // 인접 행렬과 큐와 방문 배열

void BFS(int v)
{
int i;

    visit[v] = 1; // 정점 v를 방문했다고 표시
    printf(""%d에서 시작\n"", v);
    queue[rear++] = v; // 큐에 v를 삽입하고 후단을 1 증가시킴
    while (front < rear) // 후단이 전단과 같거나 작으면 루프 탈출
    {
        // 큐의 첫번째에 있는 데이터를 제외하고 값을 가져오며, 전단 1 증가
        v = queue[front++];
        for (i = 1; i <= n; i++)
        {
            // 정점 v와 정점 i가 만나고, 정점 i를 방문하지 않은 상태일 경우
            if (map[v][i] == 1 && !visit[i])
            {
                visit[i] = 1; // 정점 i를 방문했다고 표시
                printf(""%d에서 %d로 이동\n"", v, i);
                queue[rear++] = i; // 큐에 i를 삽입하고 후단을 1 증가시킴
            }
        }
    }
}

Queue que = new Queue();
root.marked = true;
que.enqueue(root);
while(!que.isEmpty()){
    Node r = que.dequeue();
    visit®;
    foreach(Node n in r.adjacent){
        if(n.marked==false){
            n.marked = true;
            que.enqueue(n);
        }
    }
}
```


### DFS
* depth first search 깊이 탐색
```cpp
int n; // 정점의 총 갯수
int map[30][30], visit[30]; // 인접 행렬과 방문 여부
void DFS(int v)
{
    int i;

    visit[v] = 1; // 정점 v를 방문했다고 표시
    for (i = 1; i <= n; i++)
    {
        // 정점 v와 정점 i가 연결되었고, 정점 i를 방문하지 않았다면
        if (map[v][i] == 1 && !visit[i])
        {
            printf(""%d에서 %d로 이동\n"", v, i);
            // 정점 i에서 다시 DFS를 시작한다
            DFS(i);
        }
    }
}

if(root==null)return;
visit(root);
root.visited=true;
foreach(Node n in root.adjacent){
    if(n,visit == false){
        search(n);
    }
}
```

### binary tree
```cpp
// 전위 중 왼 오른 - 루트가 먼저 출력
// 중위 왼 중 오른 - 루트가 중간
// 후위 왼 오 중 - 루트가 마지막
// 레벨 큐 이용 전부 큐에 넣고 출력 그냥 줄대로 나옴
class Node:
    def __init__(self, val):
        self.val = val
        self.leftChild = None
        self.rightChild = None

class BinarySearchTree:
def __init__(self):
self.root = None

    def setRoot(self, val):
        self.root = Node(val)"	"def insert(self, val):
        if (self.root is None):
            self.setRoot(val)
        else:
            self.insertNode(self.root, val)

    def insertNode(self, currentNode, val):
        if (val <= currentNode.val):
            if (currentNode.leftChild):
                self.insertNode(currentNode.leftChild, val)
            else:
                currentNode.leftChild = Node(val)
        elif (val > currentNode.val):
            if (currentNode.rightChild):
                self.insertNode(currentNode.rightChild, val)
            else:
                currentNode.rightChild = Node(val)"	"def traverse(self):
        return self.traverseNode(self.root)

    def traverseNode(self, currentNode):
        result = []
        if (currentNode.leftChild is not None):
           result.extend(self.traverseNode(currentNode.leftChild))
        if (currentNode is not None):
            result.extend([currentNode.val])
        if (currentNode.rightChild is not None):
            result.extend(self.traverseNode(currentNode.rightChild))
        return result
```


### dijkstra
다익스트라
F = G+H
비용
시작점과 새로운점 이동비용
얻어진 사각형으로부터 대각선을 포함하지 않는 목표까지 이동거리
```cpp
    // 정점의 개수
    int V;
    // 그래프의 인접 리스트. (연결된 정점 번호, 간선 가중치) 쌍을 담는다.
    vector<pair<int, int> > adj[MAX_V];

    vector<int> dijkstra(int src) {
    vector<int> dist(V, INF);
    dist[src] = 0;
    priority_queue<pair<int, int> > pq;
    pq.push(make_pair(0, src));

    while (!pq.empty()) {
        int cost = -pq.top().first;
        int here = pq.top().second;
        pq.pop();
        // 만약 지금 꺼낸 것보다 더 짧은 경로를 알고 있다면 지금 꺼낸 것을 무시한다.
        if (dist[here] < cost) continue;

        // 인접한 정점들을 모두 검사한다.
        for (int i = 0; i < adj[here].size(); ++i) {
            int there = adj[here][i].first;
            int nextDist = cost + adj[here][i].second;
            // 더 짧은 경로를 발견하면, dist[]를 갱신하고 우선순위 큐에 넣는다.
            if (dist[there] > nextDist) {
                dist[there] = nextDist;
                pq.push(make_pair(-nextDist, there));
            }
        }
    }

    return dist;
}
```


### astar
```java
function A*(start, goal)
// 이미 실행했던 노드들 '닫힌 목록’
closedSet := {}
// 아직 실행하지 않았지만 이제 탐색할 노드들 ‘열린 목록’
// 초기에는, 시작 노드만 들어있습니다.
openSet := {start}
// 각가장 효율적인 경로를(노드들을) 담습니다.
cameFrom := the empty map
// 각 노드별 시작 노드로부터의 거리를 담습니다. (기본 비용은 Infinity, 최소비용을 찾는 것이므로)
gScore := map with default value of Infinity
// 처음 노드는 시작 노드이므로 gScore는 0입니다.
gScore[start] := 0
// 시작 노드로부터의 비용, 목적 노드까지의 비용 두 가지가 합산된 비용입니다.
fScore := map with default value of Infinity

// 첫 번째 노드는 시작 노드로부터의 비용이 0이고, 목적 노드까지는 heuristic한 추정 비용입니다.
// 그러므로, 첫 노드의 전체 비용은 추정값만 있을 뿐 입니다.
fScore[start] := heuristic_cost_estimate(start, goal)
// '열린 목록’이 비어있을 때까지 반복합니다.
while openSet is not empty
// '열린 목록’에서 가장 적은 f값을 가지는 노드
current := the node in openSet having the lowest fScore[] value
// 목적 노드입니까?
if current = goal
// 길 찾기를 완료하였으니 경로를 만듭니다.
return reconstruct_path(cameFrom, current)
// 목적노드가 아니라면 '열린 목록’에서 삭제하고 '닫힌 목록’에 넣습니다.
openSet.Remove(current)
closedSet.Add(current)
// 최소 비용으로 선택한 노드의 인접 노드들을 바라봅니다.
for each neighbor of current”	" // 인접 노드가 이미 '닫힌 목록’에 들어있다면 무시하고 넘어갑니다. (이미 실행해 본것이므로)
if neighbor in closedSet
continue
// '열린 목록’에 들어있지 않다면 추가합니다.
if neighbor not in openSet
openSet.Add(neighbor)
// current 노드까지의 gScore + current 노드로부터 인접 노드까지 거리를 구합니다.
// 시작 노드로부터 인접 노드까지 gScore가 current 노드를 거쳐
// 인접 노드까지 가는 비용보다 싸다면 이 경로는 무시합니다.
tentative_gScore := gScore[current] + dist_between(current, neighbor)
if tentative_gScore >= gScore[neighbor]
continue
// current 노드를 거쳐서 가는 것이 더 좋다고 생각되면 기록합니다.
cameFrom[neighbor] := current
gScore[neighbor] := tentative_gScore
fScore[neighbor] := gScore[neighbor] + heuristic_cost_estimate(neighbor, goal)
return failure
function reconstruct_path(cameFrom, current)
total_path := [current]
while current in cameFrom.Keys:
current := cameFrom[current]
total_path.append(current)
return total_path
```