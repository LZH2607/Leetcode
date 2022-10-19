# 【Leetcode】Floyd算法



[toc]



相关视频：
[求最短路径Floyd算法！](https://www.bilibili.com/video/BV14R4y1x7GB/)



## 815. 公交路线

![](D:\Notes\Leetcode\Leetcode.assets\815.png)

相关视频：
[花花酱 LeetCode 815. Bus Routes - 刷题找工作 EP180](https://www.youtube.com/watch?v=vEcm5farBls)

我的AC代码（Java）：

```java
class Solution {
    public int numBusesToDestination(int[][] routes, int source, int target) {
        if (source == target) {
            return 0;
        }
        final int INF = Integer.MAX_VALUE / 2;
        int n = routes.length;
        int[][] dist = new int[n][n];
        for (int[] row : dist) {
            Arrays.fill(row, INF);
        }
        Map<Integer, Set<Integer>> m = new HashMap<>();
        for (int i = 0; i < routes.length; i++) {  // 第i辆公交车
            for (int j = 0; j < routes[i].length; j++) {  // 第j个车站
                int stop = routes[i][j];
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
        for (int stop : m.keySet()) {
            Set<Integer> buses = m.get(stop);
            if (buses.size() > 1) {
                for (int bus1 : buses) {
                    for (int bus2 : buses) {
                        dist[bus1][bus2] = 1;
                    }
                }
            }
        }
        for (int i = 0; i < n; i++) {
            dist[i][i] = 0;
        }
        // Floyd算法
        for (int k = 0; k < n; k++) {
            for (int i = 0; i < n; i++) {
                for (int j = 0; j < n; j++) {
                    if (dist[i][j] > dist[i][k] + dist[k][j]) {
                        dist[i][j] = dist[i][k] + dist[k][j];
                    }
                }
            }
        }
        int minDist = Integer.MAX_VALUE;
        for (int bus1 : m.get(source)) {
            for (int bus2 : m.get(target)) {
                if (dist[bus1][bus2] < minDist) {
                    minDist = dist[bus1][bus2];
                }
            }
        }
        if (minDist == INF) {
            return -1;
        }
        return minDist + 1;
    }
}
```

