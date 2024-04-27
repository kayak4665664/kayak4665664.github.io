# LeetCode 42


[LeetCode 42.Trapping Rain Water](https://leetcode.com/problems/trapping-rain-water/description/), a very interesting problem.
&lt;!--more--&gt;

Given `n` non-negative integers representing an elevation map where the width of each bar is `1`, compute how much water it can trap after raining.

**Example:**
&lt;div align=&#34;center&#34;&gt;
{{&lt; image src=&#34;https://cdn.jsdelivr.net/gh/kayak4665664/My-images/rainwatertrap.png&#34; alt=&#34;rainwatertrap&#34; height=&#34;60%&#34; width=&#34;60%&#34;&gt;}}
&lt;/div&gt;

**Input**: height = `[0, 1, 0, 2, 1, 0, 1, 3, 2, 1, 2, 1]`  
**Output**: `6`  
**Explanation**: The above elevation map (black section) is represented by array `[0, 1, 0, 2, 1, 0, 1, 3, 2, 1, 2, 1]`. In this case, `6` units of rain water (blue section) are being trapped.

At first I wanted to solve it with `stack`, but it didn&#39;t feel good. Then I just calculated directly up and down, but `Time Limit Exceeded`:

```cpp
class Solution {
   public:
    int trap(vector&lt;int&gt;&amp; height) {
        int ans = 0;
        unordered_map&lt;int, vector&lt;int&gt;&gt; index;
        for (int i = 0; i &lt; height.size(); &#43;&#43;i) {
            for (int j = 1; j &lt;= height[i]; &#43;&#43;j) index[j].push_back(i);
        }
        for (auto p : index) {
            auto v = p.second;
            for (int i = 1; i &lt; v.size(); &#43;&#43;i) ans &#43;= v[i] - v[i - 1] - 1;
        }
        return ans;
    }
};
```

Read the reference solution and the main idea is to surround the left and right sides and find the height of the horizontal plane:
```cpp
class Solution {
   public:
    int trap(vector&lt;int&gt;&amp; height) {
        int ans = 0, l = 0, r = height.size() - 1, level = 0;
        while (l &lt; r) {
            int lower = (height[l] &gt; height[r] ? height[r--] : height[l&#43;&#43;]);
            level = max(lower, level);
            ans &#43;= level - lower;
        }
        return ans;
    }
};
```

There should be many solutions to this problem.

---

> Author: [kayak4665664](https://github.com/kayak4665664)  
> URL: https://www.kayak4665664.com/leetcode-42/  

