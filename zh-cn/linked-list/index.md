# 链表


一个双向链表的C&#43;&#43;模版。

&lt;!--more--&gt;

```cpp
#include &lt;iostream&gt;
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
    n-&gt;val = val;
    n-&gt;next = p-&gt;next;
    p-&gt;next = n;
    n-&gt;prior = p;
    if (n-&gt;next != nullptr) n-&gt;next-&gt;prior = n;
    return n;
}

void erase(ListNode *p) {
    p-&gt;prior-&gt;next = p-&gt;next;
    if (p-&gt;next != nullptr) p-&gt;next-&gt;prior = p-&gt;prior;
    delete p;
}

void print(ListNode *p) {
    if (p != nullptr) {
        cout &lt;&lt; p-&gt;val;
        p = p-&gt;next;
    }
    while (p != nullptr) {
        cout &lt;&lt; &#34; -&gt; &#34; &lt;&lt; p-&gt;val;
        p = p-&gt;next;
    }
    cout &lt;&lt; endl;
}

int main() {
    ListNode *front = new ListNode(1);
    ListNode *n = insert(insert(insert(front, 2), 4)-&gt;prior, 3);
    print(front);  // 1 -&gt; 2 -&gt; 3 -&gt; 4
    erase(n);
    print(front);  // 1 -&gt; 2 -&gt; 4
    return 0;
}
```

1. [LeetCode 21. Merge Two Sorted Lists](https://leetcode.com/problems/merge-two-sorted-lists/description/)
```cpp
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

2. [LeetCode 23. Merge k Sorted Lists](https://leetcode.com/problems/merge-k-sorted-lists/description/)

直接用这个方法导致`Time Limit Exceeded`，
```cpp
class Solution {
   public:
    ListNode *mergeKLists(vector&lt;ListNode *&gt; &amp;lists) {
        int flag = 0, min = 0x3f3f3f;
        ListNode *front, *p, *p1;
        unordered_map&lt;ListNode *, ListNode *&gt; ptr;
        vector&lt;ListNode *&gt; ps;
        for (auto list : lists) {
            if (list != nullptr) {
                flag = 1;
                ptr[list] = list;
                if (list-&gt;val &lt; min) {
                    min = list-&gt;val;
                    front = list;
                }
            }
        }
        if (!lists.size() || !flag)
            return nullptr;
        else {
            ptr[front] = ptr[front]-&gt;next;
            p = front;
            while (true) {
                flag = 0, min = 0x3f3f3f;
                for (auto list : lists) {
                    if (ptr[list] != nullptr) {
                        flag = 1;
                        if (ptr[list]-&gt;val &lt; min) {
                            min = ptr[list]-&gt;val;
                            p1 = list;
                        }
                    }
                }
                if (!flag) break;
                p-&gt;next = ptr[p1];
                p = p-&gt;next;
                ptr[p1] = ptr[p1]-&gt;next;
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
    ListNode *mergeKLists(vector&lt;ListNode *&gt; &amp;lists) {
        ListNode *front, *p;
        auto cmp = [](ListNode *a, ListNode *b) {
            return a-&gt;val &gt;= b-&gt;val;
        };  // ptr.top() is minimal.
        priority_queue&lt;ListNode *, vector&lt;ListNode *&gt;, decltype(cmp)&gt; ptr(cmp);
        for (auto list : lists) {
            if (list != nullptr) ptr.push(list);
        }
        if (!lists.size() || ptr.empty())
            return nullptr;
        else {
            front = ptr.top();
            ptr.pop();
            if (front-&gt;next != nullptr) ptr.push(front-&gt;next);
            p = front;
            while (!ptr.empty()) {
                p-&gt;next = ptr.top();
                ptr.pop();
                p = p-&gt;next;
                if (p-&gt;next != nullptr) ptr.push(p-&gt;next);
            }
            return front;
        }
    }
};
```

---

> 作者: [kayak4665664](https://github.com/kayak4665664)  
> URL: https://www.kayak4665664.com/zh-cn/linked-list/  

