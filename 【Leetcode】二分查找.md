# 【Leetcode】二分查找



[toc]



## 二分查找

相关视频：
[二分查找为什么总是写错？](https://www.bilibili.com/video/BV1d54y1q7k7/)

代码模板：

```java
int binarySearch(int[] nums, int target) {
    int l_idx = -1;
    int r_idx = nums.length;
    while (l_idx + 1 < r_idx) {
        int mid_idx = (l_idx + r_idx) / 2;
        if (条件) {
            l_idx = mid_idx;
        } else {
            r_idx = mid_idx;
        }
    }
    return l_idx 或 r_idx;
}
```

| 目标 | 条件 | 返回 |
| :--: | :--: | :--: |
| 找到第一个≥target的元素 | nums[mid_idx] < target | r_idx |
| 找到第一个>target的元素 | nums[mid_idx] <= target | r_idx |
| 找到最后一个≤target的元素 | nums[mid_idx] <= target | l_idx |
| 找到最后一个<target的元素 | nums[mid_idx] < target | l_idx |



## 33. 搜索旋转排序数组（Java）

![](D:\Notes\Leetcode\Leetcode.assets\33.png)

相关视频：
[【LeetCode 每日一题】33. 搜索旋转排序数组 | 手写图解版思路 + 代码讲解](https://www.bilibili.com/video/BV1Aq4y1c7L2/)

我的AC代码（Java）：

```java
class Solution {
    public int search(int[] nums, int target) {
        int end = getRangeIndex(nums);
        int idx;
        if (target >= nums[0]) {
            idx = searchInRange(nums, 0, end, target);
        } else {
            idx = searchInRange(nums, end + 1, nums.length - 1, target);
        }
        if (!(idx >= 0 && idx < nums.length && nums[idx] == target)) {
            idx = -1;
        }
        return idx;
    }

    int getRangeIndex(int[] nums) {
        int l_idx = -1;
        int r_idx = nums.length;
        while (l_idx + 1 < r_idx) {
            int mid_idx = (l_idx + r_idx) / 2;
            if (nums[mid_idx] >= nums[0]) {
                l_idx = mid_idx;
            } else {
                r_idx = mid_idx;
            }
        }
        return l_idx;
    }

    int searchInRange(int[] nums, int l, int r, int target) {
        int l_idx = l - 1;
        int r_idx = r + 1;
        while (l_idx + 1 < r_idx) {
            int mid_idx = (l_idx + r_idx) / 2;
            if (nums[mid_idx] < target) {
                l_idx = mid_idx;
            } else {
                r_idx = mid_idx;
            }
        }
        return r_idx;
    }
}
```



## 34. 在排序数组中查找元素的第一个和最后一个位置（Java）

![](D:\Notes\Leetcode\Leetcode.assets\34.png)

相关视频：
[二分查找为什么总是写错？](https://www.bilibili.com/video/BV1d54y1q7k7/)

我的AC代码（Java）：

```java
class Solution {
    public int[] searchRange(int[] nums, int target) {
        int[] res = new int[2];
        res[0] = searchFirst(nums, target);
        res[1] = searchLast(nums, target);
        if (res[0] > res[1]) {
            Arrays.fill(res, -1);
        }
        return res;
    }

    int searchFirst(int[] nums, int target) {
        int l_idx = -1;
        int r_idx = nums.length;
        while (l_idx + 1 < r_idx) {
            int mid_dix = (l_idx + r_idx) / 2;
            if (nums[mid_dix] < target) {
                l_idx = mid_dix;
            } else {
                r_idx = mid_dix;
            }
        }
        return r_idx;
    }

    int searchLast(int[] nums, int target) {
        int l_idx = -1;
        int r_idx = nums.length;
        while (l_idx + 1 < r_idx) {
            int mid_dix = (l_idx + r_idx) / 2;
            if (nums[mid_dix] <= target) {
                l_idx = mid_dix;
            } else {
                r_idx = mid_dix;
            }
        }
        return l_idx;
    }
}
```



## 35. 搜索插入位置（Java）

![](D:\Notes\Leetcode\Leetcode.assets\35.png)

我的AC代码（Java）：

```java
class Solution {
    public int searchInsert(int[] nums, int target) {
        int l_idx = -1;
        int r_idx = nums.length;
        while (l_idx + 1 < r_idx) {
            int mid_idx = (l_idx + r_idx) / 2;
            if (nums[mid_idx] < target) {
                l_idx = mid_idx;
            } else {
                r_idx = mid_idx;
            }
        }
        return r_idx;
    }
}
```



## 278. 第一个错误的版本（Java）

![](D:\Notes\Leetcode\Leetcode.assets\278.png)

我的AC代码（Java）：

```java
public class Solution extends VersionControl {
    public int firstBadVersion(int n) {
        long l_idx = 0;
        long r_idx = (long) n + 1;
        while (l_idx + 1 < r_idx) {
            int mid_idx = (int) ((l_idx + r_idx) / 2);
            if (!isBadVersion(mid_idx)) {
                l_idx = mid_idx;
            } else {
                r_idx = mid_idx;
            }
        }
        return (int) r_idx;
    }
}
```



## 704. 二分查找（Java）

![](D:\Notes\Leetcode\Leetcode.assets\704.png)

我的AC代码（Java）：

```java
class Solution {
    public int search(int[] nums, int target) {
        int l_idx = -1;
        int r_idx = nums.length;
        while (l_idx + 1 < r_idx) {
            int mid_idx = (l_idx + r_idx) / 2;
            if (nums[mid_idx] < target) {
                l_idx = mid_idx;
            } else {
                r_idx = mid_idx;
            }
        }
        if (r_idx == nums.length || nums[r_idx] != target) {
            r_idx = -1;
        }
        return r_idx;
    }
}
```

