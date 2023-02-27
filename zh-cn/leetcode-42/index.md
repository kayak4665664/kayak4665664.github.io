# LeetCode 42


https://cdn.jsdelivr.net/gh/kayak4665664/My-images
<!--more-->

给定 `n` 个非负整数表示每个宽度为 `1` 的柱子的高度图，计算按此排列的柱子，下雨之后能接多少雨水。

**示例：**
<div align="center">
{{< image src="https://cdn.jsdelivr.net/gh/kayak4665664/My-images/rainwatertrap.png" title="rainwatertrap" alt="rainwatertrap" height="60%" width="60%">}}
</div>

**输入**：height = `[0, 1, 0, 2, 1, 0, 1, 3, 2, 1, 2, 1]`  
**输出**：`6`  
**解释**：上面是由数组 `[0, 1, 0, 2, 1, 0, 1, 3, 2, 1, 2, 1]` 表示的高度图，在这种情况下，可以接 `6` 个单位的雨水（蓝色部分表示雨水）。

刚开始想用`stack`做，不过感觉不太好。然后我就直接上下一层一层算，但是`Time Limit Exceeded`了：

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

看了看参考答案，主要思路是左右围起来并且求水平面高度：
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

这道题解法应该挺多的。

---

> 作者: [kayak4665664](https://github.com/kayak4665664)  
> URL: https://www.kayak4665664.com/zh-cn/leetcode-42/  

