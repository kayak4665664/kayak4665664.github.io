# Binary Search


This is a C&#43;&#43; template for the binary search algorithm, and a simple application of the binary search functions `std::lower_bound` and `std::upper_bound` in the C&#43;&#43; standard template library `&lt;algorithm&gt;` header file.

&lt;!--more--&gt;

```cpp
#include &lt;algorithm&gt;
#include &lt;iostream&gt;
using namespace std;

int nums[] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};

int binary_search(int left, int right, int key) {
    int pos = -1, mid;
    while (left &lt;= right) {
        mid = left &#43; (right - left) / 2;
        if (key &gt; nums[mid])
            left = mid &#43; 1;
        else if (key &lt; nums[mid])
            right = mid - 1;
        else {
            pos = mid;
            break;
        }
    }
    return pos;
}

int main() {
    cout &lt;&lt; binary_search(0, 9, 3) &lt;&lt; endl;                  // 2
    cout &lt;&lt; lower_bound(nums, nums &#43; 10, 3) - nums &lt;&lt; endl;  // 2, &gt;= 3
    cout &lt;&lt; upper_bound(nums, nums &#43; 10, 3) - nums &lt;&lt; endl;  // 3, &gt; 3
    return 0;
}
```

Used this template and completed [34. Find First and Last Position of Element in Sorted Array](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/description/) in LeetCode.

```cpp
class Solution {
   public:
    vector&lt;int&gt; searchRange(vector&lt;int&gt;&amp; nums, int target) {
        if (!nums.size())
            return vector&lt;int&gt;{-1, -1};
        else {
            int pos = binary_search(nums, 0, nums.size() - 1, target);
            if (pos == -1)
                return vector&lt;int&gt;{-1, -1};
            else {
                int left = pos - 1, right = pos &#43; 1, size = nums.size();
                while (left &gt;= 0  &amp;&amp; nums[left] == target) --left;
                while (right &lt; size &amp;&amp; nums[right] == target) &#43;&#43;right;
                return vector&lt;int&gt;{left &#43; 1, right - 1};
            }
        }
    }

    int binary_search(vector&lt;int&gt; nums, int left, int right, int key) {
        int pos = -1, mid;
        while (left &lt;= right) {
            mid = left &#43; (right - left) / 2;
            if (key &gt; nums[mid])
                left = mid &#43; 1;
            else if (key &lt; nums[mid])
                right = mid - 1;
            else {
                pos = mid;
                break;
            }
        }
        return pos;
    }
};
```


---

> Author: [kayak4665664](https://github.com/kayak4665664)  
> URL: http://localhost:1313/posts/binary-search/  

