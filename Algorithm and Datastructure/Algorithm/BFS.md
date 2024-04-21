> [!notes]
> 큐는 데이터 구조이고, BFS는 탐색 알고리즘 중 하나
# 큐와 BFS

##### 노드의 처리 순서
첫 번째 라운드에서는 루트 노드를 처리합니다. 두 번째 라운드에서는 루트 노드에 인접한 노드를 처리하고, 세 번째 라운드에서는 루트 노드에서 두 단계 떨어진 노드를 처리하는 식으로 처리합니다.  
  
트리의 레벨 순서 탐색과 유사하게 루트 노드에 가까운 노드가 먼저 탐색됩니다.  
  
k번째 라운드에서 노드 X가 큐에 추가되면 루트 노드와 X 사이의 최단 경로의 길이는 정확히 k입니다. 즉, 대상 노드를 처음 찾을 때 이미 최단 경로에 있는 것입니다.

##### 큐의 대기열 추가 및 대기열 해제 순서
위의 애니메이션과 같이 먼저 루트 노드를 큐에 넣습니다. 그런 다음 각 라운드에서 이미 대기열에 있는 노드를 하나씩 처리하고 그 이웃 노드를 모두 대기열에 추가합니다. 새로 추가된 노드는 즉시 트래버스되지 않고 다음 라운드에서 처리된다는 점에 주목할 필요가 있습니다.  
  
노드의 처리 순서는 대기열에 추가된 방식과 정확히 동일한 순서인 선입선출(FIFO) 방식입니다. 이것이 바로 BFS에서 큐를 사용하는 이유입니다.

![[Queue]]

## Template
```java
/**
 * Return the length of the shortest path between root and target node.
 */
int BFS(Node root, Node target) {
    Queue<Node> queue;  // store all nodes which are waiting to be processed
    int step = 0;       // number of steps needed from root to current node
    // initialize
    add root to queue;
    // BFS
    while (queue is not empty) {
        // iterate the nodes which are already in the queue
        int size = queue.size();
        for (int i = 0; i < size; ++i) {
            Node cur = the first node in queue;
            return step if cur is target;
            for (Node next : the neighbors of cur) {
                add next to queue;
            }
            remove the first node from queue;
        }
        step = step + 1;
    }
    return -1;          // there is no path from root to target
}
```

```ts
class Node {
// java의 큐를 직접 구현하여 큐의 기능을 모방함
// 실제 구현에서는 이웃 노드들을 저장하는 방식(예: 배열, 연결 리스트 등)을 정의해야함
  neighbors: Node[];

  constructor() {
    this.neighbors = [];
  }
}

function BFS(root: Node, target: Node): number {
  let queue: Node[] = []; // 모든 노드를 저장하는 큐
  let step: number = 0; // root에서 현재 노드까지 필요한 단계 수

  queue.push(root);

  
  
}
```