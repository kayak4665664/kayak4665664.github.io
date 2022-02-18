# LeetCode 42


[LeetCode 42.Trapping Rain Water](https://leetcode.com/problems/trapping-rain-water/description/), a very interesting problem.
<!--more-->

Given `n` non-negative integers representing an elevation map where the width of each bar is `1`, compute how much water it can trap after raining.

**Example:**
<div align="center">
{{< image src="https://cdn.kayak4665664.com/rainwatertrap.png" title="rainwatertrap" alt="rainwatertrap" height="60%" width="60%">}}
</div>
<code><pre><strong>Input</strong>: height = [0,1,0,2,1,0,1,3,2,1,2,1]
<strong>Output</strong>: 6
<strong>Explanation</strong>: The above elevation map (black section) is represented by array [0,1,0,2,1,0,1,3,2,1,2,1]. In this case, 6 units of rain water (blue section) are being trapped.
</code></pre>

At first I wanted to solve it with `stack`, but it didn't feel good. Then I just calculated directly up and down, but `Time Limit Exceeded`:

```cpp
class Solution {
   public:
    int trap(vector<int>& height) {
        int ans = 0;
        unordered_map<int, vector<int>> index;
        for (int i = 0; i < height.size(); ++i) {
            for (int j = 1; j <= height[i]; ++j) index[j].push_back(i);
        }
        for (auto p : index) {
            auto v = p.second;
            for (int i = 1; i < v.size(); ++i) ans += v[i] - v[i - 1] - 1;
        }
        return ans;
    }
};
```

Read the reference solution and the main idea is to surround the left and right sides and find the height of the horizontal plane:
```cpp
class Solution {
   public:
    int trap(vector<int>& height) {
        int ans = 0, l = 0, r = height.size() - 1, level = 0;
        while (l < r) {
            int lower = (height[l] > height[r] ? height[r--] : height[l++]);
            level = max(lower, level);
            ans += level - lower;
        }
        return ans;
    }
};
```

There should be many solutions to this problem.
