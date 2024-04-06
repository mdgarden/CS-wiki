---
tags:
  - Linked_List
  - Algorithm
  - Datastructure
---
```
/** * Definition for singly-linked list. 
* class ListNode { 
* val: number 
* next: ListNode | null 
* constructor(val?: number, next?: ListNode | null) { 
* this.val = (val===undefined ? 0 : val) 
* this.next = (next===undefined ? null : next) 
*     }
*   }
* /
```

이걸 생성하려면 하단과 같이 쓴다.

```ts
let node3 = new ListNode(3);
let node2 = new ListNode(2, node3);
let head = new ListNode(1, node2);
```

실제로 생성된 객체의 모습은 이렇다.

```ts
// 첫 번째 노드
let head = {
    val: 1,
    next: {
        val: 2,
        next: {
        
            val: 3,
            next: null  // 리스트의 마지막 노드는 다음 노드가 없으므로 null
        }
    }
};

```