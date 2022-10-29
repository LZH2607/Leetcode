# 【Leetcode】优先队列



[toc]



## 1845. 座位预约管理系统

![](D:\Notes\Leetcode\Leetcode.assets\1845.png)

我的AC代码（Java）：

```java
class SeatManager {
    Queue<Integer> q;

    public SeatManager(int n) {
        q = new PriorityQueue<>();
        for (int i = 1; i <= n; i++) {
            q.offer(i);
        }
    }

    public int reserve() {
        return q.poll();
    }

    public void unreserve(int seatNumber) {
        q.offer(seatNumber);
    }
}
```

