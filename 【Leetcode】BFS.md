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

