# 二分查找


这是二分查找算法的一个C&#43;&#43;模版，以及C&#43;&#43;标准模版库`&lt;algorithm&gt;`头文件中二分查找函数`std::lower_bound`和`std::upper_bound`的简单应用。

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

用这个模版做了一道LeetCode的[34. Find First and Last Position of Element in Sorted Array](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/description/)。

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

> 作者: [kayak4665664](https://github.com/kayak4665664)  
> URL: http://localhost:1313/zh-cn/posts/binary-search/  

