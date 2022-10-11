# 【Leetcode】单调栈



[toc]



## 84. 柱状图中最大的矩形

![](D:\Notes\Leetcode\Leetcode.assets\84.png)

相关视频：
[84. 柱状图中最大的矩形 Largest Rectangle in Histogram 【LeetCode 力扣官方题解】](https://www.bilibili.com/video/BV16D4y1D7ed/)
[求柱状图中最大的矩形 ，经典难题，快来挑战一下吧！](https://www.bilibili.com/video/BV1hN4y1V7rV/)
[【LeetCode 每日一题】84. 柱状图中最大的矩形 | 手写图解版思路 + 代码讲解](https://www.bilibili.com/video/BV1dY4y1q7tL/)

我的AC代码（Java，解法1）：

```java
class Solution {
    int len;
    int[] l_idx;
    int[] r_idx;

    public int largestRectangleArea(int[] heights) {
        len = heights.length;
        l_idx = new int[len];
        r_idx = new int[len];
        getRightIndex(heights);
        getLeftIndex(heights);
        int maxArea = 0;
        for (int i = 0; i < len; i++) {
            int area = heights[i] * (r_idx[i] - l_idx[i] + 1);
            if (area > maxArea) {
                maxArea = area;
            }
        }
        return maxArea;
    }

    void getRightIndex(int[] heights) {
        Deque<Integer> d = new ArrayDeque<>();
        for (int i = 0; i < len; i++) {
            int cur = heights[i];
            while (!d.isEmpty()) {
                int last = heights[d.getFirst()];
                if (cur < last) {
                    r_idx[d.pop()] = i - 1;
                    continue;
                }
                break;
            }
            d.push(i);
        }
        while (!d.isEmpty()) {
            r_idx[d.pop()] = len - 1;
        }
    }

    void getLeftIndex(int[] heights) {
        Deque<Integer> d = new ArrayDeque<>();
        for (int i = len - 1; i >= 0; i--) {
            int cur = heights[i];
            while (!d.isEmpty()) {
                int last = heights[d.getFirst()];
                if (cur < last) {
                    l_idx[d.pop()] = i + 1;
                    continue;
                }
                break;
            }
            d.push(i);
        }
        while (!d.isEmpty()) {
            l_idx[d.pop()] = 0;
        }
    }
}
```

我的AC代码（Java，解法2）：

```java
class Solution {
    public int largestRectangleArea(int[] heights) {
        Deque<Integer> d = new ArrayDeque<>();
        int len = heights.length;
        int maxArea = 0;
        for (int i = 0; i < len; i++) {
            int cur = heights[i];
            while (!d.isEmpty()) {
                int last = heights[d.getFirst()];
                if (cur < last) {
                    d.pop();
                    int w = d.isEmpty() ? i : i - d.getFirst() - 1;
                    int area = last * w;
                    if (area > maxArea) {
                        maxArea = area;
                    }
                    continue;
                }
                break;
            }
            d.push(i);
        }
        while (!d.isEmpty()) {
            int h = heights[d.pop()];
            int w = d.isEmpty() ? len : len - d.getFirst() - 1;
            int area = h * w;
            if (area > maxArea) {
                maxArea = area;
            }
        }
        return maxArea;
    }
}
```



## 85. 最大矩形

![](D:\Notes\Leetcode\Leetcode.assets\85.png)

相关视频：
[【LeetCode 每日一题】85. 最大矩形 | 手写图解版思路 + 代码讲解](https://www.bilibili.com/video/BV1NS4y1m7zW/)

我的AC代码（Java）：

```java
class Solution {
    int row;
    int col;
    int len;
    int[] heights;

    public int maximalRectangle(char[][] matrix) {
        row = matrix.length;
        if (row == 0) {
            return 0;
        }
        col = matrix[0].length;
        len = col;
        heights = new int[len];
        int maxArea = 0;
        for (int r = 0; r < row; r++) {
            getHeights(matrix, r);
            int area = getMaxArea();
            if (area > maxArea) {
                maxArea = area;
            }
        }
        return maxArea;
    }

    void getHeights(char[][] matrix, int r) {
        // 默认当前的heights是r-1的
        int col = matrix[r].length;
        for (int c = 0; c < col; c++) {
            if (matrix[r][c] == '1') {
                heights[c]++;
            } else {  // matrix[r][c] == '0'
                heights[c] = 0;
            }
        }
    }

    int getMaxArea() {
        Deque<Integer> d = new ArrayDeque<>();
        int maxArea = 0;
        for (int i = 0; i < len; i++) {
            int cur = heights[i];
            while (!d.isEmpty()) {
                int last = heights[d.getFirst()];
                if (cur < last) {
                    d.pop();
                    int w = d.isEmpty() ? i : i - d.getFirst() - 1;
                    int area = last * w;
                    if (area > maxArea) {
                        maxArea = area;
                    }
                    continue;
                }
                break;
            }
            d.push(i);
        }
        while (!d.isEmpty()) {
            int h = heights[d.pop()];
            int w = d.isEmpty() ? len : len - d.getFirst() - 1;
            int area = h * w;
            if (area > maxArea) {
                maxArea = area;
            }
        }
        return maxArea;
    }
}
```



## 503. 下一个更大元素 II

![](D:\Notes\Leetcode\Leetcode.assets\503.png)

我的AC代码：

```java
class Solution {
    public int[] nextGreaterElements(int[] nums) {
        Deque<Integer> d = new ArrayDeque<>();
        int len = nums.length;
        int[] ans = new int[len];
        Arrays.fill(ans, Integer.MIN_VALUE);
        if (len == 1) {
            ans[0] = -1;
            return ans;
        }
        for (int n = 0; n < 2; n++) {  // 2轮
            for (int i = 0; i < len; i++) {
                int cur = nums[i];
                while (!d.isEmpty()) {
                    int last = nums[d.getFirst()];
                    if (cur > last) {
                        ans[d.pop()] = cur;
                        continue;
                    }
                    break;
                }
                d.push(i);
            }
        }
        while (!d.isEmpty()) {
            int i = d.pop();
            if (ans[i] == Integer.MIN_VALUE) {
                ans[i] = -1;
            }
        }
        return ans;
    }
}
```



## 739. 每日温度

![](D:\Notes\Leetcode\Leetcode.assets\739.png)

相关视频：
[739. 每日温度 Daily Temperatures【LeetCode 力扣官方题解】](https://www.bilibili.com/video/BV1ov411z7rM/)

我的AC代码（Java）：

```java
class Solution {
    public int[] dailyTemperatures(int[] temperatures) {
        Deque<Integer> d = new ArrayDeque<>();
        int len = temperatures.length;
        int[] days = new int[len];
        if (len == 1) {
            return days;
        }
        for (int i = 0; i < len; i++) {
            int cur = temperatures[i];
            while (!d.isEmpty()) {
                int last = temperatures[d.getFirst()];
                if (cur > last) {
                    int j = d.pop();
                    days[j] = i - j;
                    continue;
                }
                break;
            }
            d.push(i);
        }
        while (!d.isEmpty()) {
            days[d.pop()] = 0;
        }
        return days;
    }
}
```



## 901. 股票价格跨度

![](D:\Notes\Leetcode\Leetcode.assets\901.png)

相关视频：
[LeetCode 每日一题 Daily Challenge 901 Online Stock Span](https://www.youtube.com/watch?v=ZTelsIrE11w/)

我的AC代码：

```java
class StockSpanner {
    Deque<int[]> d = new ArrayDeque<>();

    public StockSpanner() {

    }

    public int next(int price) {
        if (d.isEmpty()) {
            int[] arr = {price, 1};
            d.push(arr);
            return d.getFirst()[1];
        }
        int cnt = 1;
        while (!d.isEmpty()) {
            if (d.getFirst()[0] <= price) {
                cnt += d.getFirst()[1];
                d.pop();
                continue;
            }
            break;
        }
        int[] arr = {price, cnt};
        d.push(arr);
        return d.getFirst()[1];
    }
}
```

