# 【Leetcode】队列



[toc]



## 933. 最近的请求次数

![](D:\Notes\Leetcode\Leetcode.assets\933.png)

我的AC代码（Java）：

```java
class RecentCounter {
    Deque<Integer> d;

    public RecentCounter() {
        d = new ArrayDeque<>();
    }

    public int ping(int t) {
        d.push(t);
        while (true) {
            if (d.getLast() < t - 3000) {
                d.pollLast();
            } else {
                break;
            }
        }
        return d.size();
    }
}
```

