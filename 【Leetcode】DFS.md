# 【Leetcode】DFS



相关视频：
[[Python] BFS和DFS算法（第1讲）](https://www.bilibili.com/video/BV1Ks411579J/)
[[Python] BFS和DFS算法（第2讲）](https://www.bilibili.com/video/BV1Ks411575U/)
[数据结构-浙江大学](https://www.bilibili.com/video/BV1JW411i731/)



[toc]



## 130. 被围绕的区域

![](D:\Notes\Leetcode\Leetcode.assets\130.png)

相关视频：
[【LeetCode 每日一题】130. 被围绕的区域 | 手写图解版思路 + 代码讲解](https://www.bilibili.com/video/BV1DY4y1r71T/)

我的AC代码（Java）：

```java
class Solution {
    char[][] board;
    int m;
    int n;
    boolean[][] visit;
    int[] dr = {-1, 0, 1, 0};
    int[] dc = {0, 1, 0, -1};

    public void solve(char[][] board) {
        this.board = board;
        m = board.length;
        n = board[0].length;
        visit = new boolean[m][n];
        for (int r = 0; r < m; r++) {
            if (board[r][0] == 'O') {
                dfs(r, 0);
            }
            if (board[r][n - 1] == 'O') {
                dfs(r, n - 1);
            }
        }
        for (int c = 0; c < n; c++) {
            if (board[0][c] == 'O') {
                dfs(0, c);
            }
            if (board[m - 1][c] == 'O') {
                dfs(m - 1, c);
            }
        }
        for (int r = 0; r < m; r++) {
            for (int c = 0; c < n; c++) {
                if (!visit[r][c]) {
                    board[r][c] = 'X';
                }
            }
        }
    }

    void dfs(int r, int c) {
        if (r < 0 || r >= m || c < 0 || c >= n) {
            return;
        }
        if (board[r][c] != 'O' || visit[r][c]) {
            return;
        }
        visit[r][c] = true;
        for (int i = 0; i < 4; i++) {
            dfs(r + dr[i], c + dc[i]);
        }
    }
}
```



## 924. 尽量减少恶意软件的传播

![](D:\Notes\Leetcode\Leetcode.assets\924.png)

我的AC代码（Java）：

```java
class Solution {
    List<List<Integer>> ll;
    int n;
    boolean[] visit;
    int[] initial;
    int M;
    int minM;
    int res;

    public int minMalwareSpread(int[][] graph, int[] initial) {
        init(graph, initial);
        for (int i : initial) {
            reset();
            for (int j : initial) {
                if (i == j) {
                    continue;
                }
                dfs(j);
            }
            if (M < minM) {
                minM = M;
                res = i;
            } else if (M == minM && i < res) {
                res = i;
            }
        }
        return res;
    }

    void init(int[][] graph, int[] initial) {
        ll = new ArrayList<>();
        n = graph.length;
        for (int i = 0; i < n; i++) {
            List<Integer> l = new ArrayList<>();
            for (int j = 0; j < n; j++) {
                if (graph[i][j] != 0 && i != j) {
                    l.add(j);
                }
            }
            ll.add(l);
        }
        visit = new boolean[n];
        this.initial = initial;
        M = 0;
        minM = Integer.MAX_VALUE;
    }

    void reset() {
        Arrays.fill(visit, false);
        M = 0;
    }

    void dfs(int i) {
        if (visit[i]) {
            return;
        }
        visit[i] = true;
        M++;
        List<Integer> neighbors = ll.get(i);
        for (int neighbor : neighbors) {
            dfs(neighbor);
        }
    }
}
```



## 934. 最短的桥

![](D:\Notes\Leetcode\Leetcode.assets\934.png)

我的AC代码（Java）：

```java
import java.util.Collection;

class Solution {
    int[][] grid;
    int n;
    final int ISLAND = 1;
    final int SEA = 0;
    final int FROM = -1;
    final int TO = 1;
    boolean[][] visit;
    int[][] cnt;
    int[] dr = {-1, 0, 1, 0};
    int[] dc = {0, 1, 0, -1};
    List<int[]> l;
    Deque<int[]> d;
    int minCnt;

    public int shortestBridge(int[][] grid) {
        init(grid);
        setFrom();
        getTo();
        setCnt();
        for (int[] coordinate : l) {
            if (cnt[coordinate[0]][coordinate[1]] - 1 < minCnt) {
                minCnt = cnt[coordinate[0]][coordinate[1]] - 1;
            }
        }
        return minCnt;
    }

    void init(int[][] grid) {
        this.grid = grid;
        n = grid.length;
        visit = new boolean[n][n];
        cnt = new int[n][n];
        for (int[] row : cnt) {
            Arrays.fill(row, Integer.MAX_VALUE);
        }
        l = new ArrayList<>();
        d = new ArrayDeque<>();
        minCnt = Integer.MAX_VALUE;
    }

    void setFrom() {
        for (int r = 0; r < n; r++) {
            for (int c = 0; c < n; c++) {
                if (grid[r][c] == ISLAND) {
                    dfs(r, c, l);
                    for (boolean[] row : visit) {
                        Arrays.fill(row, false);
                    }
                    for (int[] coordinate : l) {
                        grid[coordinate[0]][coordinate[1]] = FROM;
                    }
                    return;
                }
            }
        }
    }

    void getTo() {
        for (int r = 0; r < n; r++) {
            for (int c = 0; c < n; c++) {
                if (grid[r][c] == TO) {
                    dfs(r, c, d);
                    for (boolean[] row : visit) {
                        Arrays.fill(row, false);
                    }
                    return;
                }
            }
        }
    }

    void dfs(int r, int c, Collection<int[]> col) {
        if (r < 0 || r >= n || c < 0 || c >= n) {
            return;
        }
        if (grid[r][c] == SEA || visit[r][c]) {
            return;
        }
        visit[r][c] = true;
        int[] coordinate = {r, c};
        col.add(coordinate);
        for (int i = 0; i < 4; i++) {
            dfs(r + dr[i], c + dc[i], col);
        }
    }

    void setCnt() {
        while (!d.isEmpty()) {
            int r = d.getLast()[0];
            int c = d.getLast()[1];
            d.pollLast();
            if (r < 0 || r >= n || c < 0 || c >= n) {
                continue;
            }
            if (cnt[r][c] != Integer.MAX_VALUE) {
                continue;
            }
            if (grid[r][c] == TO) {
                cnt[r][c] = 0;
            } else {
                for (int i = 0; i < 4; i++) {
                    cnt[r][c] = Math.min(getCnt(r + dr[i], c + dc[i]), cnt[r][c]);
                }
                cnt[r][c]++;
            }
            for (int i = 0; i < 4; i++) {
                int[] coordinate = {r + dr[i], c + dc[i]};
                d.addFirst(coordinate);
            }
        }
    }

    int getCnt(int r, int c) {
        if (r < 0 || r >= n || c < 0 || c >= n) {
            return Integer.MAX_VALUE;
        }
        return cnt[r][c];
    }
}
```

