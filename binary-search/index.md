# Binary Search


This is a C++ template for the binary search algorithm, and a simple application of the binary search functions `std::lower_bound` and `std::upper_bound` in the C++ standard template library `<algorithm>` header file.

<!--more-->

```cpp
#include <algorithm>
#include <iostream>
using namespace std;

int nums[] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};

int binary_search(int left, int right, int key) {
    int pos = -1, mid;
    while (left <= right) {
        mid = left + (right - left) / 2;
        if (key > nums[mid])
            left = mid + 1;
        else if (key < nums[mid])
            right = mid - 1;
        else {
            pos = mid;
            break;
        }
    }
    return pos;
}

int main() {
    cout << binary_search(0, 9, 3) << endl;                  // 2
    cout << lower_bound(nums, nums + 10, 3) - nums << endl;  // 2, >= 3
    cout << upper_bound(nums, nums + 10, 3) - nums << endl;  // 3, > 3
    return 0;
}
```

Used this template and completed [34. Find First and Last Position of Element in Sorted Array](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/description/) in LeetCode.

```cpp
class Solution {
   public:
    vector<int> searchRange(vector<int>& nums, int target) {
        if (!nums.size())
            return vector<int>{-1, -1};
        else {
            int pos = binary_search(nums, 0, nums.size() - 1, target);
            if (pos == -1)
                return vector<int>{-1, -1};
            else {
                int left = pos - 1, right = pos + 1, size = nums.size();
                while (left >= 0  && nums[left] == target) --left;
                while (right < size && nums[right] == target) ++right;
                return vector<int>{left + 1, right - 1};
            }
        }
    }

    int binary_search(vector<int> nums, int left, int right, int key) {
        int pos = -1, mid;
        while (left <= right) {
            mid = left + (right - left) / 2;
            if (key > nums[mid])
                left = mid + 1;
            else if (key < nums[mid])
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
> URL: https://www.kayak4665664.com/binary-search/  

