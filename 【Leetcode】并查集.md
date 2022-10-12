# 【Leetcode】并查集



[toc]



## 200. 岛屿数量

![](D:\Notes\Leetcode\Leetcode.assets\200.png)

我的AC代码（Java）：

```java
class Solution {
    int row;
    int col;
    int len;
    int[] parent;
    char[][] grid;

    public int numIslands(char[][] grid) {
        init(grid);
        for (int r = 1; r < row - 1; r++) {
            for (int c = 1; c < col - 1; c++) {
                if (this.grid[r][c] == '0') {
                    continue;
                }
                List<Coordinate> neighbors = getNeighbors(r, c);
                for (Coordinate neighbor : neighbors) {
                    int root1 = find(getIndex(r, c));
                    int root2 = find(getIndex(neighbor.r, neighbor.c));
                    if (root1 < root2) {
                        parent[root1] += parent[root2];
                        parent[root2] = root1;
                    } else if (root1 > root2) {
                        parent[root2] += parent[root1];
                        parent[root1] = root2;
                    }
                }
            }
        }
        Set<Integer> s = new HashSet<>();
        for (int r = 1; r < row - 1; r++) {
            for (int c = 1; c < col - 1; c++) {
                if (this.grid[r][c] == '0') {
                    continue;
                }
                s.add(find(getIndex(r, c)));
            }
        }
        return s.size();
    }

    void init(char[][] grid) {
        row = grid.length + 2;
        col = grid[0].length + 2;
        this.grid = new char[row][col];
        for (int r = 0; r < row; r++) {
            Arrays.fill(this.grid[r], '0');
        }
        for (int r = 0; r < grid.length; r++) {
            System.arraycopy(grid[r], 0, this.grid[r + 1], 1, grid[r].length);
        }
        len = row * col;
        parent = new int[len];
        Arrays.fill(parent, -1);
    }

    int getIndex(int r, int c) {
        return r * col + c;
    }

    List<Coordinate> getNeighbors(int r, int c) {
        List<Coordinate> l = new ArrayList<>();
        if (this.grid[r][c - 1] == '1') {  // 左
            l.add(new Coordinate(r, c - 1));
        }
        if (this.grid[r - 1][c] == '1') {  // 上
            l.add(new Coordinate(r - 1, c));
        }
        if (this.grid[r][c + 1] == '1') {  // 右
            l.add(new Coordinate(r, c + 1));
        }
        if (this.grid[r + 1][c] == '1') {  // 下
            l.add(new Coordinate(r + 1, c));
        }
        return l;
    }

    int find(int i) {
        return parent[i] < 0 ? i : find(parent[i]);
    }
}

class Coordinate {
    int r;
    int c;

    Coordinate(int r, int c) {
        this.r = r;
        this.c = c;
    }
}
```



## 261. 以图判树

![](D:\Notes\Leetcode\Leetcode.assets\261.png)

我的AC代码（Java）：

```java
class Solution {
    int[] parent;

    public boolean validTree(int n, int[][] edges) {
        parent = new int[n];
        Arrays.fill(parent, -1);
        boolean flag = true;
        for (int[] edge : edges) {
            int root1 = find(edge[0]);
            int root2 = find(edge[1]);
            if (root1 < root2) {
                parent[root1] += parent[root2];
                parent[root2] = root1;
            } else if (root1 > root2) {
                parent[root2] += parent[root1];
                parent[root1] = root2;
            } else {  // root1 == root2
                flag = false;
                break;
            }
        }
        if (flag) {
            int cnt = 0;
            for (int i = 0; i < n; i++) {
                if (parent[i] < 0 && cnt == 0) {
                    cnt++;
                } else if (parent[i] < 0 && cnt > 0) {
                    flag = false;
                    break;
                }
            }
        }
        return flag;
    }

    int find(int i) {
        return parent[i] < 0 ? i : find(parent[i]);
    }
}
```



## 323. 无向图中连通分量的数目

![](D:\Notes\Leetcode\Leetcode.assets\323.png)

我的AC代码（Java）：

```java
class Solution {
    int[] parent;

    public int countComponents(int n, int[][] edges) {
        parent = new int[n];
        Arrays.fill(parent, -1);
        for (int[] edge : edges) {
            int root1 = find(edge[0]);
            int root2 = find(edge[1]);
            if (root1 < root2) {
                parent[root1] += parent[root2];
                parent[root2] = root1;
            } else if (root1 > root2) {
                parent[root2] += parent[root1];
                parent[root1] = root2;
            }
        }
        int cnt = 0;
        for (int i = 0; i < n; i++) {
            if (parent[i] < 0) {
                cnt++;
            }
        }
        return cnt;
    }

    int find(int i) {
        return parent[i] < 0 ? i : find(parent[i]);
    }
}
```



## 547. 省份数量

![](D:\Notes\Leetcode\Leetcode.assets\547.png)

我的AC代码（Java）：

```java
class Solution {
    int len;
    int[] parent;

    public int findCircleNum(int[][] isConnected) {
        len = isConnected.length;
        parent = new int[len];
        Arrays.fill(parent, -1);
        for (int i = 0; i < len; i++) {
            for (int j = 0; j < len; j++) {
                if (i == j || isConnected[i][j] == 0) {
                    continue;
                }
                int root1 = find(i);
                int root2 = find(j);
                if (root1 < root2) {
                    parent[root1] += parent[root2];
                    parent[root2] = root1;
                } else if (root1 > root2) {
                    parent[root2] += parent[root1];
                    parent[root1] = root2;
                }
            }
        }
        int cnt = 0;
        for (int i = 0; i < len; i++) {
            if (parent[i] < 0) {
                cnt++;
            }
        }
        return cnt;
    }

    int find(int i) {
        return parent[i] < 0 ? i : find(parent[i]);
    }
}
```



## 684. 冗余连接

![](D:\Notes\Leetcode\Leetcode.assets\684.png)

我的AC代码（Java）：

```java
class Solution {
    int len;
    int[] parent;

    public int[] findRedundantConnection(int[][] edges) {
        len = edges.length;
        parent = new int[len + 1];
        Arrays.fill(parent, -1);
        int[] ans = null;
        for (int[] edge : edges) {
            int root1 = find(edge[0]);
            int root2 = find(edge[1]);
            if (root1 < root2) {
                parent[root1] += parent[root2];
                parent[root2] = root1;
            } else if (root1 > root2) {
                parent[root2] += parent[root1];
                parent[root1] = root2;
            } else {  // root1 == root2
                ans = edge;
                break;
            }
        }
        return ans;
    }

    int find(int i) {
        return parent[i] < 0 ? i : find(parent[i]);
    }
}
```



## 737. 句子相似性 II

![](D:\Notes\Leetcode\Leetcode.assets\737.png)

我的AC代码（Java）：

```java
class Solution {
    Map<String, String> parent;

    public boolean areSentencesSimilarTwo(String[] sentence1, String[] sentence2, List<List<String>> similarPairs) {
        if (sentence1.length != sentence2.length) {
            return false;
        }
        parent = new HashMap<>();
        for (List<String> pair : similarPairs) {
            String s1 = pair.get(0);
            String s2 = pair.get(1);
            if (!parent.containsKey(s1)) {
                parent.put(s1, s1);
            }
            if (!parent.containsKey(s2)) {
                parent.put(s2, s2);
            }
            String root1 = find(s1);
            String root2 = find(s2);
            if (root1.hashCode() > root2.hashCode()) {
                parent.put(root2, root1);
            } else if (root1.hashCode() < root2.hashCode()) {
                parent.put(root1, root2);
            }
        }
        boolean flag = true;
        for (int i = 0; i < sentence1.length; i++) {
            if (!find(sentence1[i]).equals(find(sentence2[i]))) {
                flag = false;
                break;
            }
        }
        return flag;
    }

    String find(String s) {
        return !parent.containsKey(s) || parent.get(s).equals(s) ? s : find(parent.get(s));
    }
}
```



## 1061. 按字典序排列最小的等效字符串

![](D:\Notes\Leetcode\Leetcode.assets\1061.png)

我的AC代码（Java）：

```java
class Solution {
    int len;
    int[] parent;

    public String smallestEquivalentString(String s1, String s2, String baseStr) {
        parent = new int[256];
        Arrays.fill(parent, -1);
        char[] arr1 = s1.toCharArray();
        char[] arr2 = s2.toCharArray();
        len = arr1.length;
        for (int i = 0; i < len; i++) {
            if (arr1[i] == arr2[i]) {
                continue;
            }
            int root1 = find((int) arr1[i]);
            int root2 = find((int) arr2[i]);
            if (root1 < root2) {
                parent[root2] = root1;
            } else if (root1 > root2) {
                parent[root1] = root2;
            }
        }
        char[] arr3 = baseStr.toCharArray();
        for (int i = 0; i < arr3.length; i++) {
            arr3[i] = (char) find((int) arr3[i]);
        }
        return new String(arr3);
    }

    int find(int i) {
        return parent[i] < 0 ? i : find(parent[i]);
    }
}
```