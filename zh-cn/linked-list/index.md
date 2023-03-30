# 链表


一个双向链表的C++模版。

<!--more-->

```cpp
#include <iostream>
using namespace std;

struct ListNode {
    int val;
    ListNode *next, *prior;
    ListNode() : val(0), next(nullptr), prior(nullptr) {}
    ListNode(int v) : val(v), next(nullptr), prior(nullptr) {}
    ListNode(int v, ListNode *next, ListNode *prior)
        : val(v), next(next), prior(prior) {}
};

ListNode *insert(ListNode *p, int val) {
    ListNode *n = new ListNode;
    n->val = val;
    n->next = p->next;
    p->next = n;
    n->prior = p;
    if (n->next != nullptr) n->next->prior = n;
    return n;
}

void erase(ListNode *p) {
    p->prior->next = p->next;
    if (p->next != nullptr) p->next->prior = p->prior;
    delete p;
}

void print(ListNode *p) {
    if (p != nullptr) {
        cout << p->val;
        p = p->next;
    }
    while (p != nullptr) {
        cout << " -> " << p->val;
        p = p->next;
    }
    cout << endl;
}

int main() {
    ListNode *front = new ListNode(1);
    ListNode *n = insert(insert(insert(front, 2), 4)->prior, 3);
    print(front);  // 1 -> 2 -> 3 -> 4
    erase(n);
    print(front);  // 1 -> 2 -> 4
    return 0;
}
```

1. [LeetCode 21. Merge Two Sorted Lists](https://leetcode.com/problems/merge-two-sorted-lists/description/)
```cpp
class Solution {
   public:
    ListNode* mergeTwoLists(ListNode* list1, ListNode* list2) {
        if (list1 == nullptr && list2 == nullptr)
            return nullptr;
        else if (list1 == nullptr)
            return list2;
        else if (list2 == nullptr)
            return list1;
        else {
            ListNode *front, *p, *p1, *p2;
            if (list1->val <= list2->val) {
                front = list1;
                p1 = list1->next;
                p2 = list2;
            } else {
                front = list2;
                p1 = list1;
                p2 = list2->next;
            }
            p = front;
            while (p1 != nullptr && p2 != nullptr) {
                if (p1->val <= p2->val) {
                    p->next = p1;
                    p1 = p1->next;
                } else {
                    p->next = p2;
                    p2 = p2->next;
                }
                p = p->next;
            }
            if (p1 == nullptr)
                p->next = p2;
            else
                p->next = p1;
            return front;
        }
    }
};
```

2. [LeetCode 23. Merge k Sorted Lists](https://leetcode.com/problems/merge-k-sorted-lists/description/)

直接用这个方法导致`Time Limit Exceeded`，
```cpp
class Solution {
   public:
    ListNode *mergeKLists(vector<ListNode *> &lists) {
        int flag = 0, min = 0x3f3f3f;
        ListNode *front, *p, *p1;
        unordered_map<ListNode *, ListNode *> ptr;
        vector<ListNode *> ps;
        for (auto list : lists) {
            if (list != nullptr) {
                flag = 1;
                ptr[list] = list;
                if (list->val < min) {
                    min = list->val;
                    front = list;
                }
            }
        }
        if (!lists.size() || !flag)
            return nullptr;
        else {
            ptr[front] = ptr[front]->next;
            p = front;
            while (true) {
                flag = 0, min = 0x3f3f3f;
                for (auto list : lists) {
                    if (ptr[list] != nullptr) {
                        flag = 1;
                        if (ptr[list]->val < min) {
                            min = ptr[list]->val;
                            p1 = list;
                        }
                    }
                }
                if (!flag) break;
                p->next = ptr[p1];
                p = p->next;
                ptr[p1] = ptr[p1]->next;
            }
            return front;
        }
    }
};
```

用优先队列就可以通过了。
```cpp
class Solution {
   public:
    ListNode *mergeKLists(vector<ListNode *> &lists) {
        ListNode *front, *p;
        auto cmp = [](ListNode *a, ListNode *b) {
            return a->val >= b->val;
        };  // ptr.top() is minimal.
        priority_queue<ListNode *, vector<ListNode *>, decltype(cmp)> ptr(cmp);
        for (auto list : lists) {
            if (list != nullptr) ptr.push(list);
        }
        if (!lists.size() || ptr.empty())
            return nullptr;
        else {
            front = ptr.top();
            ptr.pop();
            if (front->next != nullptr) ptr.push(front->next);
            p = front;
            while (!ptr.empty()) {
                p->next = ptr.top();
                ptr.pop();
                p = p->next;
                if (p->next != nullptr) ptr.push(p->next);
            }
            return front;
        }
    }
};
```

---

> 作者: [kayak4665664](https://github.com/kayak4665664)  
> URL: https://www.kayak4665664.com/zh-cn/linked-list/  

