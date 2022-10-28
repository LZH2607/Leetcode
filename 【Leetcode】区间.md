# 【Leetcode】区间



[toc]



## 56. 合并区间

![](D:\Notes\Leetcode\Leetcode.assets\56.png)

我的AC代码（Java）：

```java
class Solution {
    Deque<int[]> d;
    Deque<int[]> temp;

    public int[][] merge(int[][] intervals) {
        d = new ArrayDeque<>();
        temp = new ArrayDeque<>();
        for (int[] interval : intervals) {
            addInterval(interval);
        }
        int[][] res = new int[d.size()][];
        int i = 0;
        while (!d.isEmpty()) {
            res[i] = d.pop();
            i++;
        }
        return res;
    }

    void addInterval(int[] interval) {
        while (!d.isEmpty() && d.getFirst()[0] > interval[0]) {
            temp.push(d.pop());
        }
        push(interval);
        while (!temp.isEmpty()) {
            push(temp.pop());
        }
    }

    void push(int[] interval) {
        if (d.isEmpty()) {
            d.push(interval);
            return;
        }
        // !d.isEmpty()
        if (d.getFirst()[1] >= interval[0]) {
            d.getFirst()[1] = Math.max(d.getFirst()[1], interval[1]);
        } else {  // d.getFirst()[1] < interval[0]
            d.push(interval);
        }
    }
}
```



## 57. 插入区间

![](D:\Notes\Leetcode\Leetcode.assets\57.png)

我的AC代码（Java）：

```java
class Solution {
    Deque<int[]> d;
    Deque<int[]> temp;

    public int[][] insert(int[][] intervals, int[] newInterval) {
        d = new ArrayDeque<>();
        temp = new ArrayDeque<>();
        for (int[] interval : intervals) {
            addInterval(interval);
        }
        addInterval(newInterval);
        int[][] res = new int[d.size()][];
        int i = 0;
        while (!d.isEmpty()) {
            res[i] = d.pollLast();
            i++;
        }
        return res;
    }

    void addInterval(int[] interval) {
        while (!d.isEmpty() && d.getFirst()[0] > interval[0]) {
            temp.push(d.pop());
        }
        push(interval);
        while (!temp.isEmpty()) {
            push(temp.pop());
        }
    }

    void push(int[] interval) {
        if (d.isEmpty()) {
            d.push(interval);
            return;
        }
        // !d.isEmpty()
        if (d.getFirst()[1] >= interval[0]) {
            d.getFirst()[1] = Math.max(d.getFirst()[1], interval[1]);
        } else {  // d.getFirst()[1] < interval[0]
            d.push(interval);
        }
    }
}
```



## 763. 划分字母区间

![](D:\Notes\Leetcode\Leetcode.assets\763.png)

相关视频：
[花花酱 LeetCode 763. Partition Labels - 刷题找工作 EP161](https://www.youtube.com/watch?v=s-1W5FDJ0lw)

我的AC代码（Java）：

```java
class Solution {
    int[] l_idx;
    int[] r_idx;
    Deque<int[]> d;
    Deque<int[]> temp;
    List<Integer> l;

    public List<Integer> partitionLabels(String s) {
        init();
        for (int i = 0; i < s.length(); i++) {
            int idx = s.charAt(i) - 'a';
            if (l_idx[idx] == -1) {
                l_idx[idx] = i;
                r_idx[idx] = i;
            } else {  // l_idx[idx] != -1
                r_idx[idx] = i;
            }
        }
        for (int i = 0; i < 26; i++) {
            if (l_idx[i] == -1 && r_idx[i] == -1) {
                continue;
            }
            // l_idx[i] != -1 && r_idx[i] != -1
            int[] partition = {l_idx[i], r_idx[i]};
            addPartition(partition);
        }
        while (!d.isEmpty()) {
            int[] partition = d.pollLast();
            l.add(partition[1] - partition[0] + 1);
        }
        return l;
    }

    void init() {
        l_idx = new int[26];
        r_idx = new int[26];
        Arrays.fill(l_idx, -1);
        Arrays.fill(r_idx, -1);
        d = new ArrayDeque<>();
        temp = new ArrayDeque<>();
        l = new ArrayList<>();
    }

    void addPartition(int[] partition) {
        while (!d.isEmpty() && d.getFirst()[0] > partition[0]) {
            temp.push(d.pop());
        }
        push(partition);
        while (!temp.isEmpty()) {
            push(temp.pop());
        }
    }

    void push(int[] partition) {
        if (d.isEmpty()) {
            d.push(partition);
            return;
        }
        // !d.isEmpty()
        if (d.getFirst()[1] >= partition[0]) {
            d.getFirst()[1] = Math.max(d.getFirst()[1], partition[1]);
        } else {  // d.getFirst()[1] < partition[0]
            d.push(partition);
        }
    }
}
```



## 768. 最多能完成排序的块 II

![](D:\Notes\Leetcode\Leetcode.assets\768.png)

我的AC代码（Java）：

```java
class Solution {
    Deque<int[]> d;
    Deque<int[]> temp;
    Map<Integer, List<List<Integer>>> m;

    public int maxChunksToSorted(int[] arr) {
        int[] sortedArr = Arrays.copyOf(arr, arr.length);
        Arrays.sort(sortedArr);
        m = new HashMap<>();
        for (int i = 0; i < arr.length; i++) {
            if (m.containsKey(arr[i])) {
                m.get(arr[i]).get(0).add(i);
                continue;
            }
            List<Integer> l1 = new ArrayList<>();
            List<Integer> l2 = new ArrayList<>();
            List<List<Integer>> ll = new ArrayList<>();
            l1.add(i);
            ll.add(l1);
            ll.add(l2);
            m.put(arr[i], ll);
        }
        for (int i = 0; i < sortedArr.length; i++) {
            m.get(sortedArr[i]).get(1).add(i);
        }
        d = new ArrayDeque<>();
        temp = new ArrayDeque<>();
        for (int num : m.keySet()) {
            List<Integer> l1 = m.get(num).get(0);
            List<Integer> l2 = m.get(num).get(1);
            for (int i = l1.size() - 1; i >= 0; i--) {
                int[] interval = {l1.get(i), l2.get(i)};
                Arrays.sort(interval);
                addInterval(interval);
            }
        }
        return d.size();
    }

    void addInterval(int[] interval) {
        while (!d.isEmpty() && d.getFirst()[0] > interval[0]) {
            temp.push(d.pop());
        }
        push(interval);
        while (!temp.isEmpty()) {
            push(temp.pop());
        }
    }

    void push(int[] interval) {
        if (d.isEmpty()) {
            d.push(interval);
            return;
        }
        if (d.getFirst()[1] >= interval[0]) {
            d.getFirst()[1] = Math.max(d.getFirst()[1], interval[1]);
        } else {
            d.push(interval);
        }
    }
}
```



## 769. 最多能完成排序的块

![](D:\Notes\Leetcode\Leetcode.assets\769.png)

相关视频：
[花花酱 LeetCode 769. Max Chunks To Make Sorted - 刷题找工作 EP164](https://www.youtube.com/watch?v=twYLu4hEKnQ)

我的AC代码（Java）：

```java
class Solution {
    Map<Integer, int[]> m;
    Deque<int[]> d;
    Deque<int[]> temp;

    public int maxChunksToSorted(int[] arr) {
        int[] sortedArr = Arrays.copyOf(arr, arr.length);
        Arrays.sort(sortedArr);
        m = new HashMap<>();
        for (int i = 0; i < arr.length; i++) {
            int[] interval = new int[2];
            interval[0] = arr[i];
            m.put(i, interval);
        }
        for (int i = 0; i < sortedArr.length; i++) {
            m.get(sortedArr[i])[1] = i;
        }
        d = new ArrayDeque<>();
        temp = new ArrayDeque<>();
        for (int num : m.keySet()) {
            int[] interval = m.get(num);
            Arrays.sort(interval);
            addinterval(interval);
        }
        return d.size();
    }

    void addinterval(int[] interval) {
        while (!d.isEmpty() && d.getFirst()[0] > interval[0]) {
            temp.push(d.pop());
        }
        push(interval);
        while (!temp.isEmpty()) {
            push(temp.pop());
        }
    }

    void push(int[] interval) {
        if (d.isEmpty()) {
            d.push(interval);
            return;
        }
        if (d.getFirst()[1] >= interval[0]) {
            d.getFirst()[1] = Math.max(d.getFirst()[1], interval[1]);
        } else {
            d.push(interval);
        }
    }
}
```



## 1288. 删除被覆盖区间

![](D:\Notes\Leetcode\Leetcode.assets\1288.png)

我的AC代码（Java）：

```java
class Solution {
    Deque<int[]> d;
    Deque<int[]> temp;
    int cnt;

    public int removeCoveredIntervals(int[][] intervals) {
        d = new ArrayDeque<>();
        temp = new ArrayDeque<>();
        cnt = 0;
        for (int[] interval : intervals) {
            addInterval(interval);
        }
        return intervals.length - cnt;
    }

    void addInterval(int[] interval) {
        while (!d.isEmpty() && d.getFirst()[0] > interval[0]) {
            temp.push(d.pop());
        }
        push(interval);
        while (!temp.isEmpty()) {
            push(temp.pop());
        }
    }

    void push(int[] interval) {
        if (d.isEmpty()) {
            d.push(interval);
            return;
        }
        if (d.getFirst()[0] < interval[0] && d.getFirst()[1] < interval[1]) {
            d.push(interval);
        } else {
            d.getFirst()[1] = Math.max(d.getFirst()[1], interval[1]);
            cnt++;
        }
    }
}
```

