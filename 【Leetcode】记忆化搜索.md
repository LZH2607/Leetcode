# 【Leetcode】记忆化搜索



[toc]



## 64. 最小路径和

![](D:\Notes\Leetcode\Leetcode.assets\64.png)

我的AC代码（Java）：

```java
class Solution {
    int[][] grid;
    int m;
    int n;
    int[][] minSum;
    int[] dr = {0, 1};
    int[] dc = {1, 0};

    public int minPathSum(int[][] grid) {
        init(grid);
        return getMinSum(0, 0);
    }

    void init(int[][] grid) {
        this.grid = grid;
        m = grid.length;
        n = grid[0].length;
        minSum = new int[m][n];
        for (int r = 0; r < m; r++) {
            Arrays.fill(minSum[r], -1);
        }
    }

    int getMinSum(int r, int c) {
        if (r < 0 || r >= m || c < 0 || c >= n) {
            return Integer.MAX_VALUE;
        } else if (r == m - 1 && c == n - 1) {
            minSum[r][c] = grid[r][c];
        } else if (minSum[r][c] < 0) {
            minSum[r][c] = grid[r][c] + Math.min(getMinSum(r + dr[0], c + dc[0]), getMinSum(r + dr[1], c + dc[1]));
        }
        return minSum[r][c];
    }
}
```

