# 【Leetcode】最小生成树



[toc]



相关视频：
[最小生成树(Kruskal(克鲁斯卡尔)和Prim(普里姆))算法动画演示](https://www.bilibili.com/video/BV1Eb41177d1/)



最小生成树的算法：
	Kruskal算法
	Prim算法



## 1135. 最低成本联通所有城市

![](D:\Notes\Leetcode\Leetcode.assets\1135.png)

我的AC代码（Java）：

```java
class Solution {
    int n;
    List<int[]> l;
    int[] parent;
    int cnt;
    int cost;

    public int minimumCost(int n, int[][] connections) {
        init(n, connections);
        // Kruskal算法
        while (cnt < n - 1 && !l.isEmpty()) {
            int[] connection = l.remove(0);
            int root1 = find(connection[0]);
            int root2 = find(connection[1]);
            if (root1 == root2) {
                continue;
            }
            // root1 != root2
            if (parent[root1] <= parent[root2]) {
                parent[root1] += parent[root2];
                parent[root2] = root1;
            } else {  // parent[root1] > parent[root2]
                parent[root2] += parent[root1];
                parent[root1] = root2;
            }
            cost += connection[2];
            cnt++;
        }
        if (cnt < n - 1) {
            return -1;
        }
        return cost;
    }

    void init(int n, int[][] connections) {
        this.n = n;
        l = new ArrayList<>();
        l.addAll(Arrays.asList(connections));
        Collections.sort(l, new Comparator<int[]>() {
            public int compare(int[] connection1, int[] connection2) {
                if (connection1[2] != connection2[2]) {
                    return connection1[2] - connection2[2];
                } else if (connection1[0] != connection2[0]) {
                    return connection1[0] - connection2[0];
                }
                return connection1[1] - connection2[1];
            }
        });
        parent = new int[n + 1];
        Arrays.fill(parent, -1);
        cnt = 0;
        cost = 0;
    }

    int find(int i) {
        return parent[i] < 0 ? i : find(parent[i]);
    }
}
```

