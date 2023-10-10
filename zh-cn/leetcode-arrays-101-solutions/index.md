# Leetcode Arrays 101 题解

[Leetcode Arrays 101](https://leetcode.com/explore/learn/card/fun-with-arrays/)
<!--more-->

### [485. Max Consecutive Ones](https://leetcode.com/problems/max-consecutive-ones/description/)
```typescript
const findMaxConsecutiveOnes = (nums: number[]): number => {
  let res = 0, len = 0, end = nums.length;
  for (let i = 0; i < end; ++i) {
    if (nums[i] == 1) ++len;
    else {
      res = Math.max(res, len);
      len = 0;
    }
  }
  res = Math.max(res, len);
  return res;
};
```

### [1295. Find Numbers with Even Number of Digits](https://leetcode.com/problems/find-numbers-with-even-number-of-digits/description/)
```typescript
const findMaxConsecutiveOnes = (nums: number[]): number => {
  let res = 0, len = 0, end = nums.length;
  for (let i = 0; i < end; ++i) {
    if (nums[i] == 1) ++len;
    else {
      res = Math.max(res, len);
      len = 0;
    }
  }
  res = Math.max(res, len);
  return res;
};
```

### [977. Squares of a Sorted Array](https://leetcode.com/problems/squares-of-a-sorted-array/description/)
```typescript
function sortedSquares(nums: number[]): number[] {
  nums = nums.map(num => num * num);
  nums.sort((a, b) => a - b);
  return nums;
};
```

### [1089. Duplicate Zeros](https://leetcode.com/problems/duplicate-zeros/description/)
```typescript
/**
 Do not return anything, modify arr in-place instead.
 */
function duplicateZeros ( arr: number[] ): void {
  let i = 0, len = arr.length;
  while ( i < len ) {
    if ( arr[ i ] != 0 ) ++i;
    else {
      arr.splice( i, 0, 0 );
      arr.pop();
      i += 2;
    }
  }
};
```

### [88. Merge Sorted Array](https://leetcode.com/problems/merge-sorted-array/description/)
```typescript
/**
 Do not return anything, modify nums1 in-place instead.
 */
 function merge ( nums1: number[], m: number, nums2: number[], n: number ): void {
  let i = 0, end = m;
  for ( let num of nums2 ) {
    while ( i < end && nums1[ i ] < num ) ++i;
    nums1.splice( i, 0, num );
    nums1.pop();
    ++end;
  }
};
```

### [27. Remove Element](https://leetcode.com/problems/remove-element/description/)
```typescript
function removeElement ( nums: number[], val: number ): number {
  let res = 0, i = 0;
  while ( i < nums.length ) {
    if ( nums[ i ] != val ) {
      ++res;
      ++i;
    }
    else nums.splice( i, 1 );
  }
  return res;
};
```

### [26. Remove Duplicates from Sorted Array](https://leetcode.com/problems/remove-duplicates-from-sorted-array/description/)
```typescript
function removeDuplicates(nums: number[]): number {
  const set: Set<number> = new Set();
  let i = 0;
  while (i < nums.length) {
    if (set.has(nums[i])) nums.splice(i, 1);
    else {
      set.add(nums[i]);
      ++i;
    }
  }
  return nums.length;
};
```

### [1346. Check If N and Its Double Exist](https://leetcode.com/problems/check-if-n-and-its-double-exist/description/)
```typescript
function checkIfExist(arr: number[]): boolean {
  let res = false;
  const set: Set<number> = new Set(arr);
  const zeros = arr.filter(num => num == 0);
  const len = zeros.length;
  for (let s of set) {
    if (set.has(2 * s)) {
      if (s == 0 && len < 2) continue;
      res = true;
      break;
    }
  }
  return res;
};
```

### [941. Valid Mountain Array](https://leetcode.com/problems/valid-mountain-array/description/)
```typescript
function validMountainArray(arr: number[]): boolean {
  let res = true, inc = true, len = arr.length;
  if (len < 3 || arr[0] >= arr[1] ) return false;
  for (let i = 0; i < len; ++i) {
    if (inc && (arr[i] < arr[i - 1])) inc = false;
    if (arr[i] == arr[i - 1] || (!inc && (arr[i] >= arr[i - 1]))) {
      res = false;
      break;
    }
  }
  if (inc) res = false;
  return res;
};
```

### [1299. Replace Elements with Greatest Element on Right Side](https://leetcode.com/problems/replace-elements-with-greatest-element-on-right-side/description/)
```typescript
function replaceElements(arr: number[]): number[] {
  let res: number[] = [], len = arr.length;
  for (let i = 0; i < len - 1; ++i) {
    let max = Math.max(...arr.slice(i + 1, len));
    res.push(max);
  }
  res.push(-1);
  return res;
};
```

### [26. Remove Duplicates from Sorted Array](https://leetcode.com/problems/remove-duplicates-from-sorted-array/description/)
```typescript
function removeDuplicates(nums: number[]): number {
  const set: Set<number> = new Set();
  let i = 0;
  while (i < nums.length) {
    if (set.has(nums[i])) nums.splice(i, 1);
    else {
      set.add(nums[i]);
      ++i;
    }
  }
  return nums.length;
};
```

### [283. Move Zeroes](https://leetcode.com/problems/move-zeroes/description/)
```typescript
/**
 Do not return anything, modify nums in-place instead.
 */
function moveZeroes ( nums: number[] ): void {
  let i = 0, j = 1, len = nums.length;
  while ( i < len && j < len ) {
    if ( nums[ i ] == 0 && nums[ j ] != 0 ) {
      let temp = nums[ i ];
      nums[ i ] = nums[ j ];
      nums[ j ] = temp;

    }
    if ( nums[ i ] != 0 ) ++i;
    if ( j < i ) j = i;
    else if ( nums[ j ] == 0 ) ++j
  }
};
```

### [905. Sort Array By Parity](https://leetcode.com/problems/sort-array-by-parity/description/)
```typescript
function sortArrayByParity(nums: number[]): number[] {
  let res: number[] = [];
  res = nums.sort((a, b) => {
    if (a % 2 == 0 && b % 2 != 0) return -1;
    else if (a % 2 != 0 && b % 2 == 0) return 1;
    else return 0;
  });
  return res;
};
```

### [27. Remove Element](https://leetcode.com/problems/remove-element/description/)
```typescript
function removeElement ( nums: number[], val: number ): number {
  let res = 0, i = 0;
  while ( i < nums.length ) {
    if ( nums[ i ] != val ) {
      ++res;
      ++i;
    }
    else nums.splice( i, 1 );
  }
  return res;
};
```

### [1051. Height Checker](https://leetcode.com/problems/height-checker/description/)
```typescript
function heightChecker(heights: number[]): number {
  let res = 0, len = heights.length;
  const temp = [...heights];
  heights.sort((a, b) => a - b);
  for (let i = 0; i < len; ++i) {
    if (temp[i] != heights[i]) ++res;
  }
  return res;
};
```

### [414. Third Maximum Number](https://leetcode.com/problems/third-maximum-number/description/)
```typescript
function thirdMax ( nums: number[] ): number {
  let a = -Infinity, b = -Infinity, c = -Infinity;
  for ( let n of nums ) {
    if ( n > a || n > b && n < a || n > c && n < b ) c = n;
    if ( c > b ) {
      let t = c;
      c = b;
      b = t;
    }
    if ( b > a ) {
      let t = b;
      b = a;
      a = t;
    }
  }
  if ( c != -Infinity ) return c;
  else return a;
};
```

### [448. Find All Numbers Disappeared in an Array](https://leetcode.com/problems/find-all-numbers-disappeared-in-an-array/description/)
```typescript
function findDisappearedNumbers(nums: number[]): number[] {
  const len = nums.length, s: Set<number> = new Set(nums), res: number[] = [];
  for (let i = 1; i <= len; ++i) {
    if (!s.has(i)) res.push(i);
  }
  return res;
};
```

### [977. Squares of a Sorted Array](https://leetcode.com/problems/squares-of-a-sorted-array/description/)
```typescript
function sortedSquares(nums: number[]): number[] {
  nums = nums.map(num => num * num);
  nums.sort((a, b) => a - b);
  return nums;
};
```

---

> 作者: [kayak4665664](https://github.com/kayak4665664)  
> URL: https://www.kayak4665664.com/zh-cn/leetcode-arrays-101-solutions/  

