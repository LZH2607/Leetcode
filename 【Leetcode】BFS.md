# 【Leetcode】BFS



相关视频：
[[Python] BFS和DFS算法（第1讲）](https://www.bilibili.com/video/BV1Ks411579J/)
[[Python] BFS和DFS算法（第2讲）](https://www.bilibili.com/video/BV1Ks411575U/)
[数据结构-浙江大学](https://www.bilibili.com/video/BV1JW411i731/)



[toc]



## 815. 公交路线

![](D:\Notes\Leetcode\Leetcode.assets\815.png)

相关视频：
[花花酱 LeetCode 815. Bus Routes - 刷题找工作 EP180](https://www.youtube.com/watch?v=vEcm5farBls)

我的AC代码（Java）：

```java
class Solution {
    public int numBusesToDestination(int[][] routes, int source, int target) {
        Map<Integer, Set<Integer>> m = new HashMap<>();
        Map<Integer, Integer> cnt = new HashMap<>();
        for (int i = 0; i < routes.length; i++) {  // 第i辆公交车
            for (int j = 0; j < routes[i].length; j++) {  // 第j个车站
                int stop = routes[i][j];
                cnt.put(stop, -1);
                if (!m.containsKey(stop)) {
                    Set<Integer> s = new HashSet<>();
                    s.add(i);
                    m.put(stop, s);
                    continue;
                }
                // m.containsKey(stop)
                m.get(stop).add(i);
            }
        }
        if (!m.containsKey(source) || !m.containsKey(target)) {
            return -1;
        }
        Deque<Integer> d = new ArrayDeque<>();
        boolean flag = false;
        d.addFirst(source);
        cnt.put(source, 0);
        while (!d.isEmpty()) {
            int s = d.pollLast();
            int c = cnt.get(s);
            Set<Integer> buses = m.get(s);
            for (int bus : buses) {
                int[] stops = routes[bus];
                for (int stop : stops) {
                    if (cnt.get(stop) != -1) {
                        continue;
                    }
                    cnt.put(stop, c + 1);
                    d.addFirst(stop);
                    if (stop == target) {
                        flag = true;
                        break;
                    }
                }
            }
            if (flag) {
                break;
            }
        }
        return cnt.get(target);
    }
}
```



## 1197. 进击的骑士

![](D:\Notes\Leetcode\Leetcode.assets\1197.png)

我的AC代码（Java）：

```java
class Solution {
    public int minKnightMoves(int x, int y) {
        if (x < 0) {
            x = -x;
        }
        if (y < 0) {
            y = -y;
        }
        // 将(0, 0) → (x, y)变换为(1, 1) → (x+1, y+1)
        x++;
        y++;
        int m = 400;
        int n = 400;
        boolean[][] visit = new boolean[m][n];
        int[] dx = {2, 1, -1, -2, -2, -1, 1, 2};
        int[] dy = {1, 2, 2, 1, -1, -2, -2, -1};
        Deque<Coordinate> d = new ArrayDeque<>();
        d.push(new Coordinate(1, 1, 0));
        int minMoves = 0;
        while (!d.isEmpty()) {
            Coordinate coordinate = d.pollLast();
            if (coordinate.x < 0 || coordinate.x >= m || coordinate.y < 0 || coordinate.y >= n) {
                continue;
            }
            if (visit[coordinate.x][coordinate.y]) {
                continue;
            }
            visit[coordinate.x][coordinate.y] = true;
            if (coordinate.x == x && coordinate.y == y) {
                minMoves = coordinate.moves;
                break;
            }
            for (int i = 0; i < 8; i++) {
                d.push(new Coordinate(coordinate.x + dx[i], coordinate.y + dy[i], coordinate.moves + 1));
            }
        }
        return minMoves;
    }
}

class Coordinate {
    int x;
    int y;
    int moves;

    Coordinate(int x, int y, int moves) {
        this.x = x;
        this.y = y;
        this.moves = moves;
    }
}
```

