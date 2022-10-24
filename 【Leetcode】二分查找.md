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



## 33. 搜索旋转排序数组

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



## 34. 在排序数组中查找元素的第一个和最后一个位置

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



## 35. 搜索插入位置

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



## 278. 第一个错误的版本

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



## 704. 二分查找

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



## 933. 最近的请求次数

![](D:\Notes\Leetcode\Leetcode.assets\933.png)

我的AC代码（Java）：

```java
class RecentCounter {
    int[] arr;
    int idx;

    public RecentCounter() {
        arr = new int[10000];
        idx = 0;
    }

    public int ping(int t) {
        arr[idx] = t;
        idx++;
        // 二分查找
        int l_idx = -1;
        int r_idx = idx;
        while (l_idx + 1 < r_idx) {
            int mid_idx = (l_idx + r_idx) / 2;
            if (arr[mid_idx] < t - 3000) {
                l_idx = mid_idx;
            } else {
                r_idx = mid_idx;
            }
        }
        return idx - r_idx;
    }
}
```



## 1102. 得分最高的路径

![](D:\Notes\Leetcode\Leetcode.assets\1102.png)

相关视频：
[【LeetCode】1102. Path With Maximum Minimum Value](https://www.bilibili.com/video/BV1j34y1p7Mu/)

我的AC代码（Java）：

```java
class Solution {
    int[][] grid;
    int m;
    int n;
    List<Integer> l;
    int len;
    int minimum;
    boolean[][] visit;
    int[] dr = {-1, 0, 1, 0};
    int[] dc = {0, 1, 0, -1};

    public int maximumMinimumPath(int[][] grid) {
        init(grid);
        // 二分搜索
        int l_idx = -1;
        int r_idx = len;
        while (l_idx + 1 < r_idx) {
            int mid_idx = (l_idx + r_idx) / 2;
            minimum = l.get(mid_idx);
            resetVisit();
            if (dfs(0, 0)) {
                l_idx = mid_idx;
            } else {
                r_idx = mid_idx;
            }
        }
        return l.get(l_idx);
    }

    void init(int[][] grid) {
        this.grid = grid;
        m = grid.length;
        n = grid[0].length;
        visit = new boolean[m][n];
        Set<Integer> s = new HashSet<>();
        for (int[] row : grid) {
            for (int i : row) {
                s.add(i);
            }
        }
        l = new ArrayList<>(s);
        l.sort(Comparator.naturalOrder());
        len = l.size();
    }

    void resetVisit() {
        for (boolean[] row : visit) {
            Arrays.fill(row, false);
        }
    }

    boolean dfs(int r, int c) {
        if (r < 0 || r >= m || c < 0 || c >= n) {
            return false;
        }
        if (r == m - 1 && c == n - 1) {
            return grid[r][c] >= minimum;
        }
        if (visit[r][c] || grid[r][c] < minimum) {
            return false;
        }
        visit[r][c] = true;
        boolean flag = false;
        for (int i = 0; i < 4; i++) {
            flag = flag || dfs(r + dr[i], c + dc[i]);
        }
        return flag;
    }
}
```

