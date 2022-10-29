# 【Leetcode】前缀和



[toc]



## 42. 接雨水

![](D:\Notes\Leetcode\Leetcode.assets\42.png)

相关视频：
[Leetcode力扣 42.接雨水](https://www.bilibili.com/video/BV1zt4y197xL)

我的AC代码（Java）：

```java
class Solution {
    public int trap(int[] height) {
        int n = height.length;
        int[] l_height = new int[n];
        int[] r_height = new int[n];
        l_height[0] = 0;
        for (int i = 1; i < n; i++) {
            l_height[i] = Math.max(l_height[i - 1], height[i - 1]);
        }
        r_height[n - 1] = 0;
        for (int i = n - 2; i >= 0; i--) {
            r_height[i] = Math.max(r_height[i + 1], height[i + 1]);
        }
        int res = 0;
        for (int i = 1; i < n - 1; i++) {
            res += Math.max(0, Math.min(l_height[i], r_height[i]) - height[i]);
        }
        return res;
    }
}
```



## 238. 除自身以外数组的乘积

![](D:\Notes\Leetcode\Leetcode.assets\238.png)

相关视频：
[Leetcode 238. 除自身以外数组的乘积 前缀和](https://www.bilibili.com/video/BV1HP4y157FM)

我的AC代码（Java，解法1）：

```java
class Solution {
    public int[] productExceptSelf(int[] nums) {
        int len = nums.length;
        int[] l_product = new int[len];
        int[] r_product = new int[len];
        l_product[0] = 1;
        for (int i = 1; i < len; i++) {
            l_product[i] = l_product[i - 1] * nums[i - 1];
        }
        r_product[len - 1] = 1;
        for (int i = len - 2; i >= 0; i--) {
            r_product[i] = r_product[i + 1] * nums[i + 1];
        }
        int[] product = new int[len];
        for (int i = 0; i < len; i++) {
            product[i] = l_product[i] * r_product[i];
        }
        return product;
    }
}
```

我的AC代码（Java，解法2）：

```java
class Solution {
    public int[] productExceptSelf(int[] nums) {
        int len = nums.length;
        int[] product = new int[len];
        Arrays.fill(product, 1);
        int l_product = 1;
        for (int i = 1; i < len; i++) {
            l_product *= nums[i - 1];
            product[i] *= l_product;
        }
        int r_product = 1;
        for (int i = len - 2; i >= 0; i--) {
            r_product *= nums[i + 1];
            product[i] *= r_product;
        }
        return product;
    }
}
```



## 303. 区域和检索 - 数组不可变

![](D:\Notes\Leetcode\Leetcode.assets\303.png)

我的AC代码（Java）：

```java
class NumArray {
    int[] sum;

    public NumArray(int[] nums) {
        int len = nums.length;
        sum = new int[len];
        sum[0] = nums[0];
        for (int i = 1; i < len; i++) {
            sum[i] = sum[i - 1] + nums[i];
        }
    }

    public int sumRange(int left, int right) {
        if (left == 0) {
            return sum[right];
        }
        return sum[right] - sum[left - 1];
    }
}
```



## 304. 二维区域和检索 - 矩阵不可变

![](D:\Notes\Leetcode\Leetcode.assets\304.png)

我的AC代码（Java）：

```java
class NumMatrix {
    int[][] sum;

    public NumMatrix(int[][] matrix) {
        int m = matrix.length;
        int n = matrix[0].length;
        sum = new int[m][n];
        sum[0][0] = matrix[0][0];
        for (int col = 1; col < n; col++) {
            sum[0][col] = sum[0][col - 1] + matrix[0][col];
        }
        for (int row = 1; row < m; row++) {
            sum[row][0] = sum[row - 1][0] + matrix[row][0];
        }
        for (int row = 1; row < m; row++) {
            for (int col = 1; col < n; col++) {
                sum[row][col] = matrix[row][col] + sum[row][col - 1] + sum[row - 1][col] - sum[row - 1][col - 1];
            }
        }
    }

    public int sumRegion(int row1, int col1, int row2, int col2) {
        return getSum(row2, col2) - getSum(row2, col1 - 1) - getSum(row1 - 1, col2) + getSum(row1 - 1, col1 - 1);
    }

    int getSum(int row, int col) {
        if (row < 0 || col < 0) {
            return 0;
        }
        // row >= 0 && col >= 0
        return sum[row][col];
    }
}
```



## 334. 递增的三元子序列

![](D:\Notes\Leetcode\Leetcode.assets\334.png)

相关视频：
[【每日一题】334. Increasing Triplet Subsequence, 12/18/2020](https://www.youtube.com/watch?v=-wtypYo-K-o)

我的AC代码（Java）：

```java
class Solution {
    public boolean increasingTriplet(int[] nums) {
        int len = nums.length;
        if (len < 3) {
            return false;
        }
        int[] min = new int[len];
        int[] max = new int[len];
        min[1] = nums[0];
        for (int i = 2; i < len; i++) {
            min[i] = Math.min(nums[i - 1], min[i - 1]);
        }
        max[len - 2] = nums[len - 1];
        for (int i = len - 3; i >= 0; i--) {
            max[i] = Math.max(nums[i + 1], max[i + 1]);
        }
        for (int i = 1; i < len - 1; i++) {
            if (min[i] < nums[i] && nums[i] < max[i]) {
                return true;
            }
        }
        return false;
    }
}
```



## 523. 连续的子数组和

![](D:\Notes\Leetcode\Leetcode.assets\523.png)

我的AC代码（Java）：

```java
class Solution {
    public boolean checkSubarraySum(int[] nums, int k) {
        int len = nums.length;
        int[] sum = new int[len];
        sum[0] = nums[0];
        for (int i = 1; i < len; i++) {
            sum[i] = sum[i - 1] + nums[i];
        }
        for (int i = 0; i < len; i++) {
            sum[i] %= k;
        }
        Map<Integer, List<Integer>> m = new HashMap<>();
        for (int i = -1; i < len; i++) {
            if (i == -1) {
                List<Integer> l = new ArrayList<>();
                l.add(i);
                m.put(0, l);
                continue;
            }
            if (m.containsKey(sum[i])) {
                m.get(sum[i]).add(i);
                continue;
            }
            // !m.containsKey(sum[i])
            List<Integer> l = new ArrayList<>();
            l.add(i);
            m.put(sum[i], l);
        }
        for (int i = 0; i < len; i++) {
            if (search(m.get(sum[i]), i - 1)) {
                return true;
            }
        }
        return false;
    }

    // 用二分查找判断是否存在小于num的元素
    boolean search(List<Integer> l, int num) {
        int l_idx = -1;
        int r_idx = l.size();
        while (l_idx + 1 < r_idx) {
            int mid_idx = (l_idx + r_idx) / 2;
            if (l.get(mid_idx) < num) {
                l_idx = mid_idx;
            } else {
                r_idx = mid_idx;
            }
        }
        return l_idx > -1;
    }
}
```



## 560. 和为 K 的子数组

![](D:\Notes\Leetcode\Leetcode.assets\560.png)

相关文章：

![](D:\Notes\Leetcode\Leetcode.assets\560-solution.png)

我的AC代码（Java，解法1）：

```java
class Solution {
    public int subarraySum(int[] nums, int k) {
        int len = nums.length;
        int[] sum = new int[len];
        sum[0] = nums[0];
        for (int i = 1; i < len; i++) {
            sum[i] = sum[i - 1] + nums[i];
        }
        Map<Integer, List<Integer>> m = new HashMap<>();
        for (int i = -1; i < len; i++) {
            if (i == -1) {
                List<Integer> l = new ArrayList<>();
                l.add(i);
                m.put(0, l);
                continue;
            }
            if (m.containsKey(sum[i])) {
                m.get(sum[i]).add(i);
                continue;
            }
            // !m.containsKey(sum[i])
            List<Integer> l = new ArrayList<>();
            l.add(i);
            m.put(sum[i], l);
        }
        int cnt = 0;
        for (int i = 0; i < len; i++) {
            if (m.containsKey(sum[i] - k)) {
                cnt += count(m.get(sum[i] - k), i);
            }
        }
        return cnt;
    }

    // 用二分查找计算小于num的元素个数
    int count(List<Integer> l, int num) {
        int l_idx = -1;
        int r_idx = l.size();
        while (l_idx + 1 < r_idx) {
            int mid_idx = (l_idx + r_idx) / 2;
            if (l.get(mid_idx) < num) {
                l_idx = mid_idx;
            } else {
                r_idx = mid_idx;
            }
        }
        return l_idx + 1;
    }
}
```

我的AC代码（Java，解法2）：

```java
class Solution {
    public int subarraySum(int[] nums, int k) {
        int sum = 0;
        Map<Integer, Integer> m = new HashMap<>();
        m.put(0, 1);
        int cnt = 0;
        for (int num : nums) {
            sum += num;
            if (m.containsKey(sum - k)) {
                cnt += m.get(sum - k);
            }
            if (m.containsKey(sum)) {
                m.put(sum, m.get(sum) + 1);
            } else {  // !m.containsKey(sum)
                m.put(sum, 1);
            }
        }
        return cnt;
    }
}
```



## 974. 和可被 K 整除的子数组

![](D:\Notes\Leetcode\Leetcode.assets\974.png)

相关视频：
[974. Subarray Sums Divisible by K 和可被 K 整除的子数组【LeetCode 力扣题解】](https://www.youtube.com/watch?v=F71NLEXIUXM)

我的AC代码（Java）：

```java
class Solution {
    public int subarraysDivByK(int[] nums, int k) {
        int len = nums.length;
        int[] sum = new int[len];
        sum[0] = nums[0];
        for (int i = 1; i < len; i++) {
            sum[i] = sum[i - 1] + nums[i];
        }
        for (int i = 0; i < len; i++) {
            sum[i] %= k;
            if (sum[i] < 0) {
                sum[i] += k;
            }
        }
        Map<Integer, List<Integer>> m = new HashMap<>();
        for (int i = -1; i < len; i++) {
            if (i == -1) {
                List<Integer> l = new ArrayList<>();
                l.add(i);
                m.put(0, l);
                continue;
            }
            if (m.containsKey(sum[i])) {
                m.get(sum[i]).add(i);
                continue;
            }
            // !m.containsKey(sum[i])
            List<Integer> l = new ArrayList<>();
            l.add(i);
            m.put(sum[i], l);
        }
        int cnt = 0;
        for (int i = 0; i < len; i++) {
            cnt += count(m.get(sum[i]), i);
        }
        return cnt;
    }

    // 用二分查找计算小于num的元素个数
    int count(List<Integer> l, int num) {
        int l_idx = -1;
        int r_idx = l.size();
        while (l_idx + 1 < r_idx) {
            int mid_idx = (l_idx + r_idx) / 2;
            if (l.get(mid_idx) < num) {
                l_idx = mid_idx;
            } else {
                r_idx = mid_idx;
            }
        }
        return l_idx + 1;
    }
}
```



## 1727. 重新排列后的最大子矩阵

![](D:\Notes\Leetcode\Leetcode.assets\1727.png)

相关视频：
[【每日一题】1727. Largest Submatrix With Rearrangements, 1/18/2021](https://www.youtube.com/watch?v=_4G_266Glqk)

我的AC代码（Java）：

```java
class Solution {
    public int largestSubmatrix(int[][] matrix) {
        int m = matrix.length;
        int n = matrix[0].length;
        int[][] height = new int[m][n];
        System.arraycopy(matrix[0], 0, height[0], 0, n);
        for (int r = 1; r < m; r++) {
            for (int c = 0; c < n; c++) {
                height[r][c] = matrix[r][c] == 0 ? 0 : height[r - 1][c] + 1;
            }
        }
        int maxArea = 0;
        for (int r = 0; r < m; r++) {
            Arrays.sort(height[r]);
            for (int c = 0; c < n; c++) {
                int area = height[r][c] * (n - c);
                if (area > maxArea) {
                    maxArea = area;
                }
            }
        }
        return maxArea;
    }
}
```

