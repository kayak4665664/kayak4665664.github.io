# Leetcode Linked List 题解

[LeetCode Linked List](https://leetcode.com/explore/learn/card/linked-list/)
&lt;!--more--&gt;


### [707. Design Linked List](https://leetcode.com/problems/design-linked-list/)

```typescript
class MyLinkedList {

  val: number | undefined;
  next: MyLinkedList | undefined;
  prior: MyLinkedList | undefined;


  constructor () {
    this.val = undefined;
    this.next = undefined;
    this.prior = undefined;
  }

  get ( index: number ): number {
    if ( index == 0 ) return this.val != undefined ? this.val : -1;
    else if ( !this.next ) return -1;
    else {
      let ptr = this.next, i = 1;
      while ( i &lt; index &amp;&amp; ptr.next ) {
        ptr = ptr.next;
        &#43;&#43;i;
      }
      if ( i == index ) return ptr.val != undefined ? ptr.val : -1;
      else return -1;
    }
  }

  addAtHead ( val: number ): void {
    if ( this.val == undefined ) this.val = val;
    else {
      const next = new MyLinkedList();
      next.val = this.val;
      next.next = this.next;
      if ( next.next ) next.next.prior = next;
      next.prior = this;
      this.val = val;
      this.next = next;
      this.prior = undefined;
    }
  }

  addAtTail ( val: number ): void {
    if ( this.val == undefined ) this.val = val;
    else {
      const tail = new MyLinkedList();
      tail.val = val;
      let ptr = this.next;
      if ( !ptr ) {
        this.next = tail;
        tail.prior = this;
      } else {
        while ( ptr.next ) ptr = ptr.next;
        ptr.next = tail;
        tail.prior = ptr;
      }
    }
  }

  addAtIndex ( index: number, val: number ): void {
    if ( index == 0 ) this.addAtHead( val );
    else {
      if ( !this.next ) {
        if ( index == 1 &amp;&amp; this.val != undefined ) this.addAtTail( val );
        else return;
      } else {
        let i = 1, ptr = this.next;
        while ( i &lt; index &amp;&amp; ptr.next ) {
          &#43;&#43;i;
          ptr = ptr.next;
        }
        if ( i == index ) {
          const prior = new MyLinkedList();
          prior.val = val;
          if ( ptr.prior ) {
            ptr.prior.next = prior;
            prior.prior = ptr.prior;
          }
          prior.next = ptr;
          ptr.prior = prior;
        } else if ( i &#43; 1 == index ) {
          const tail = new MyLinkedList();
          tail.val = val;
          ptr.next = tail;
          tail.prior = ptr;
        }
      }
    }
  }


  deleteAtIndex ( index: number ): void {
    if ( index == 0 ) {
      if ( this.next ) {
        this.val = this.next.val;
        this.next = this.next.next;
        if ( this.next ) this.next.prior = this;
      } else this.val = undefined;
    } else if ( !this.next ) return;
    else {
      let i = 1, ptr = this.next;
      while ( i &lt; index &amp;&amp; ptr.next ) {
        &#43;&#43;i;
        ptr = ptr.next;
      }
      if ( i == index &amp;&amp; ptr.prior ) {
        if ( ptr.next ) {
          ptr.prior.next = ptr.next;
          ptr.next.prior = ptr.prior;
        } else ptr.prior.next = undefined;
      }
    }
  }
}

/**
 * Your MyLinkedList object will be instantiated and called as such:
 * var obj = new MyLinkedList()
 * var param_1 = obj.get(index)
 * obj.addAtHead(val)
 * obj.addAtTail(val)
 * obj.addAtIndex(index,val)
 * obj.deleteAtIndex(index)
 */
```

### [141. Linked List Cycle](https://leetcode.com/problems/linked-list-cycle/)

```typescript
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     val: number
 *     next: ListNode | null
 *     constructor(val?: number, next?: ListNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.next = (next===undefined ? null : next)
 *     }
 * }
 */

function hasCycle ( head: ListNode | null ): boolean {
  const m: Map&lt;ListNode, boolean&gt; = new Map();
  let ptr = head, res = false;
  while ( ptr !== null ) {
    if ( !m.has( ptr ) ) {
      m.set( ptr, true );
      ptr = ptr.next;
    } else {
      res = true;
      break;
    }
  }
  return res;
};
```

### [142. Linked List Cycle II](https://leetcode.com/problems/linked-list-cycle-ii/description/)
```typescript
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     val: number
 *     next: ListNode | null
 *     constructor(val?: number, next?: ListNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.next = (next===undefined ? null : next)
 *     }
 * }
 */

function detectCycle ( head: ListNode | null ): ListNode | null {
  const m: Map&lt;ListNode, boolean&gt; = new Map();
  let ptr = head, res: ListNode | null = null;
  while ( ptr !== null ) {
    if ( !m.has( ptr ) ) {
      m.set( ptr, true );
      ptr = ptr.next;
    } else {
      res = ptr;
      break;
    }
  }
  return res;
};
```

### [160. Intersection of Two Linked Lists](https://leetcode.com/problems/intersection-of-two-linked-lists/description/)
```typescript
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     val: number
 *     next: ListNode | null
 *     constructor(val?: number, next?: ListNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.next = (next===undefined ? null : next)
 *     }
 * }
 */

function getIntersectionNode ( headA: ListNode | null, headB: ListNode | null ): ListNode | null {
  let m: Map&lt;ListNode, boolean&gt; = new Map(), ptrA = headA, ptrB = headB, res: ListNode | null = null;
  while ( ptrA !== null ) {
    m.set( ptrA, true );
    ptrA = ptrA.next;
  }
  while ( ptrB !== null ) {
    if ( !m.has( ptrB ) ) {
      m.set( ptrB, true );
      ptrB = ptrB.next;
    } else {
      res = ptrB;
      break;
    }
  }
  return res;
};
```

### [19. Remove Nth Node From End of List](https://leetcode.com/problems/remove-nth-node-from-end-of-list/description/)
```typescript
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     val: number
 *     next: ListNode | null
 *     constructor(val?: number, next?: ListNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.next = (next===undefined ? null : next)
 *     }
 * }
 */

function removeNthFromEnd ( head: ListNode | null, n: number ): ListNode | null {
  let ptr = head, res: ListNode | null, list: ListNode[] = [];
  while ( ptr !== null ) {
    list.push( ptr );
    ptr = ptr.next;
  }
  let len = list.length;
  if ( n == len &amp;&amp; head ) res = head.next;
  else {
    let prior = list[ len - n - 1 ], next = n == 1 ? null : list[ len - n &#43; 1 ];
    prior.next = next;
    res = head;
  }
  return res;
};
```

### [206. Reverse Linked List](https://leetcode.com/problems/reverse-linked-list/description/)
```typescript
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     val: number
 *     next: ListNode | null
 *     constructor(val?: number, next?: ListNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.next = (next===undefined ? null : next)
 *     }
 * }
 */

function reverseList ( head: ListNode | null ): ListNode | null {
  let res: ListNode | null = null, list: ListNode[] = [], ptr = head;
  while ( ptr !== null ) {
    list.push( ptr );
    ptr = ptr.next;
  }
  let len = list.length;
  res = list[ len - 1 ] === undefined ? null : list[ len - 1 ];
  for ( let i = len - 1; i &gt; 0; --i ) {
    let prior = list[ i - 1 ], node = list[ i ];
    node.next = prior;
  }
  if ( len &gt; 0 ) list[ 0 ].next = null;
  return res;
};
```

### [203. Remove Linked List Elements](https://leetcode.com/problems/remove-linked-list-elements/description/)
```typescript
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     val: number
 *     next: ListNode | null
 *     constructor(val?: number, next?: ListNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.next = (next===undefined ? null : next)
 *     }
 * }
 */

function removeElements ( head: ListNode | null, val: number ): ListNode | null {
  let res: ListNode | null = null, list: ListNode[] = [], ptr = head;
  while ( ptr !== null ) {
    if ( ptr.val != val ) list.push( ptr );
    ptr = ptr.next;
  }
  let len = list.length;
  if ( len &gt; 0 ) res = list[ 0 ];
  for ( let i = 0; i &lt; len - 1; &#43;&#43;i )  list[ i ].next = list[ i &#43; 1 ];
  if ( len &gt; 0 ) list[ len - 1 ].next = null;
  return res;
};
```

### [328. Odd Even Linked List](https://leetcode.com/problems/odd-even-linked-list/description/)
```typescript
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     val: number
 *     next: ListNode | null
 *     constructor(val?: number, next?: ListNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.next = (next===undefined ? null : next)
 *     }
 * }
 */

function oddEvenList ( head: ListNode | null ): ListNode | null {
  let odd = head, ptr = head, oddTail: ListNode | null = head, even: ListNode | null = null, i = 1, evenTail: ListNode | null = null;
  while ( ptr !== null ) {
    if ( i % 2 != 0 ) {
      if ( i &gt; 1 &amp;&amp; oddTail ) {
        oddTail.next = ptr;
        oddTail = ptr;
      }
    } else {
      if ( i == 2 ) {
        even = ptr;
        evenTail = ptr;
      } else {
        if ( evenTail ) {
          evenTail.next = ptr;
          evenTail = ptr;
        }
      }
    }
    ptr = ptr.next;
    &#43;&#43;i;
  }
  if ( oddTail ) oddTail.next = even;
  if ( evenTail ) evenTail.next = null;
  return odd;
};
```

### [234. Palindrome Linked List](https://leetcode.com/problems/palindrome-linked-list/description/)
```typescript
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     val: number
 *     next: ListNode | null
 *     constructor(val?: number, next?: ListNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.next = (next===undefined ? null : next)
 *     }
 * }
 */

function isPalindrome ( head: ListNode | null ): boolean {
  let list: number[] = [], ptr = head, res = true;
  while ( ptr !== null ) {
    list.push( ptr.val );
    ptr = ptr.next;
  }
  let left = 0, right = list.length - 1;
  while (left &lt;= right) {
    if (list[right] != list[left]) {
      res = false;
      break;
    }
    &#43;&#43;left;
    --right;
  }
  return res;
};
```

### [21. Merge Two Sorted Lists](https://leetcode.com/problems/merge-two-sorted-lists/description/)
```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
   public:
    ListNode* mergeTwoLists(ListNode* list1, ListNode* list2) {
        if (list1 == nullptr &amp;&amp; list2 == nullptr)
            return nullptr;
        else if (list1 == nullptr)
            return list2;
        else if (list2 == nullptr)
            return list1;
        else {
            ListNode *front, *p, *p1, *p2;
            if (list1-&gt;val &lt;= list2-&gt;val) {
                front = list1;
                p1 = list1-&gt;next;
                p2 = list2;
            } else {
                front = list2;
                p1 = list1;
                p2 = list2-&gt;next;
            }
            p = front;
            while (p1 != nullptr &amp;&amp; p2 != nullptr) {
                if (p1-&gt;val &lt;= p2-&gt;val) {
                    p-&gt;next = p1;
                    p1 = p1-&gt;next;
                } else {
                    p-&gt;next = p2;
                    p2 = p2-&gt;next;
                }
                p = p-&gt;next;
            }
            if (p1 == nullptr)
                p-&gt;next = p2;
            else
                p-&gt;next = p1;
            return front;
        }
    }
};
```

### [2. Add Two Numbers](https://leetcode.com/problems/add-two-numbers/description/)
```typescript
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     val: number
 *     next: ListNode | null
 *     constructor(val?: number, next?: ListNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.next = (next===undefined ? null : next)
 *     }
 * }
 */

function addTwoNumbers ( l1: ListNode | null, l2: ListNode | null ): ListNode | null {
  let ptr1 = l1, ptr2 = l2;
  while ( ptr2 !== null || ptr1 !== null ) {
    if ( ptr2 !== null &amp;&amp; ptr1 !== null ) {
      ptr1.val &#43;= ptr2.val;
      if ( ptr1.val &gt; 9 ) {
        if ( ptr1.next ) {
          ptr1.next.val &#43;= 1;
          ptr1.val -= 10;
        } else {
          let next = new ListNode( 1 );
          ptr1.val -= 10;
          ptr1.next = next;
        }
      }
      if ( ptr2.next &amp;&amp; ptr1.next === null ) ptr1.next = new ListNode( 0 );
      ptr1 = ptr1.next;
      ptr2 = ptr2.next;
    } else if ( ptr2 === null &amp;&amp; ptr1 ) {
      if ( ptr1.val &gt; 9 ) {
        if ( ptr1.next ) {
          ptr1.next.val &#43;= 1;
          ptr1.val -= 10;
          if ( ptr1.next.val &lt; 10 ) break;
          ptr1 = ptr1.next;
        } else {
          let next = new ListNode( 1 );
          ptr1.val -= 10;
          ptr1.next = next;
        }
      } else break;
    }
  }
  return l1;
};
```

### [430. Flatten a Multilevel Doubly Linked List](https://leetcode.com/problems/flatten-a-multilevel-doubly-linked-list/description/)
```typescript
/**
 * Definition for node.
 * class Node {
 *     val: number
 *     prev: Node | null
 *     next: Node | null
 *     child: Node | null
 *     constructor(val?: number, prev? : Node, next? : Node, child? : Node) {
 *         this.val = (val===undefined ? 0 : val);
 *         this.prev = (prev===undefined ? null : prev);
 *         this.next = (next===undefined ? null : next);
 *         this.child = (child===undefined ? null : child);
 *     }
 * }
 */

function flatten ( head: Node | null ): Node | null {
  let ptr = head;
  while ( ptr !== null ) {
    if ( ptr.child ) {
      let next = ptr.next;
      let child = flatten( ptr.child );
      ptr.child = null;
      if ( child ) {
        ptr.next = child;
        child.prev = ptr;
        while ( ptr.next ) ptr = ptr.next;
        ptr.next = next;
        if ( next ) next.prev = ptr;
      }
    }
    ptr = ptr.next;
  }
  return head;
};
```

### [138. Copy List with Random Pointer](https://leetcode.com/problems/copy-list-with-random-pointer/description/)
```typescript
/**
 * Definition for Node.
 * class Node {
 *     val: number
 *     next: Node | null
 *     random: Node | null
 *     constructor(val?: number, next?: Node, random?: Node) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.next = (next===undefined ? null : next)
 *         this.random = (random===undefined ? null : random)
 *     }
 * }
 */

function copyRandomList ( head: Node | null ): Node | null {
  let res: Node | null = null, list: Node[] = [], map: Map&lt;Node, number&gt; = new Map(), ptr = head, i = 0;
  while ( ptr !== null ) {
    let node = new Node( ptr.val );
    list.push( node );
    map.set( ptr, i );
    &#43;&#43;i;
    ptr = ptr.next;
  }
  ptr = head;
  i = 0;
  while ( ptr !== null ) {
    if ( list[ i ] ) {
      list[ i &#43; 1 ] ? list[ i ].next = list[ i &#43; 1 ] : null;
      if ( ptr.random ) {
        let index = map.get( ptr.random );
        index !== undefined ? list[ i ].random = list[ index ] : null;
      } else list[ i ].random = null;
    }
    &#43;&#43;i;
    ptr = ptr.next;
  }
  res = list[ 0 ];
  return res;
};
```

### [61. Rotate List](https://leetcode.com/problems/rotate-list/description/)
```typescript
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     val: number
 *     next: ListNode | null
 *     constructor(val?: number, next?: ListNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.next = (next===undefined ? null : next)
 *     }
 * }
 */

function rotateRight ( head: ListNode | null, k: number ): ListNode | null {
  if ( k == 0 ) return head;
  let map: Map&lt;number, ListNode&gt; = new Map(), ptr = head, i = 0, res: ListNode | null = null;
  while ( ptr ) {
    map.set( i, ptr );
    ptr = ptr.next;
    &#43;&#43;i;
  }
  if ( i &lt; 2 || k % i == 0 ) return head;
  k = i - k % i;
  if ( k == 0 ) res = head;
  else {
    let node = map.get( k );
    node ? res = node : res = null;
    if ( res ) {
      ptr = res;
      while ( ptr.next ) ptr = ptr.next;
      ptr.next = head;
      ptr = head;
      while ( ptr &amp;&amp; ptr.next !== res ) ptr = ptr.next;
      if ( ptr ) ptr.next = null;
    }
  }
  return res;
};
```

---

> 作者: [kayak4665664](https://github.com/kayak4665664)  
> URL: https://www.kayak4665664.com/zh-cn/leetcode-linked-list-solutions/  

