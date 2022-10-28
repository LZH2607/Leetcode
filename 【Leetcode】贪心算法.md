# 【Leetcode】贪心算法



[toc]



相关视频：
[贪心算法巨简单？没套路？每次做题都不知道自己用了贪心？遇到简单的贪心题目靠直觉，难一点就不会了？来来来，贪心算法你该了解这些！](https://www.bilibili.com/video/BV1WK4y1R71x/)



## 45. 跳跃游戏 II

![](D:\Notes\Leetcode\Leetcode.assets\45.png)

相关视频：
[五分钟力扣 Leetcode 第45题  跳跃游戏 II 清晰易懂 例子阐述 10行代码解决一道困难题 不要错过](https://www.bilibili.com/video/BV1SA41147aU/)

我的AC代码（Java）：

```java
class Solution {
    public int jump(int[] nums) {
        int len = nums.length;
        int idx = -1;
        int max_idx = 0;
        int next_max_idx = 0;
        int cnt = 0;
        while (idx <= max_idx - 1 && max_idx < len - 1) {
            idx++;
            if (idx + nums[idx] > next_max_idx) {
                next_max_idx = idx + nums[idx];
            }
            if (idx == max_idx) {
                max_idx = next_max_idx;
                cnt++;
            }
        }
        return cnt;
    }
}
```



## 55. 跳跃游戏

![](D:\Notes\Leetcode\Leetcode.assets\55.png)

我的AC代码（Java）：

```java
class Solution {
    public boolean canJump(int[] nums) {
        int len = nums.length;
        int idx = -1;
        int max_idx = 0;
        int next_max_idx = 0;
        while (idx <= max_idx - 1 && idx < len - 1) {
            idx++;
            if (idx + nums[idx] > next_max_idx) {
                next_max_idx = idx + nums[idx];
            }
            if (idx == max_idx) {
                max_idx = next_max_idx;
            }
        }
        if (idx < len - 1) {
            return false;
        }
        return true;
    }
}
```



## 1024. 视频拼接

![](D:\Notes\Leetcode\Leetcode.assets\1024.png)

我的AC代码（Java）：

```java
class Solution {
    public int videoStitching(int[][] clips, int time) {
        Map<Integer, Integer> m = new HashMap<>();
        for (int[] clip : clips) {
            int start = clip[0];
            int end = clip[1];
            if (!m.containsKey(start)) {
                m.put(start, end);
            } else {
                m.put(start, Math.max(m.get(start), end));
            }
        }
        List<int[]> l = new ArrayList<>();
        for (int start : m.keySet()) {
            int[] clip = {start, m.get(start)};
            l.add(clip);
        }
        l.sort(new Comparator<int[]>() {
            public int compare(int[] clip1, int[] clip2) {
                if (clip1[0] != clip2[0]) {
                    return clip1[0] - clip2[0];
                }
                // clip1[0] == clip2[0]
                return clip1[1] - clip2[1];
            }
        });
        Deque<int[]> d = new ArrayDeque<>(l);
        int max_time = 0;
        int cnt = 0;
        while (!d.isEmpty() && max_time < time) {
            int next_max_time = -1;
            while (!d.isEmpty() && d.getFirst()[0] <= max_time) {
                next_max_time = Math.max(next_max_time, d.pop()[1]);
            }
            if (next_max_time == -1) {
                cnt = -1;
                break;
            }
            max_time = next_max_time;
            cnt++;
        }
        if (max_time < time) {
            cnt = -1;
        }
        return cnt;
    }
}
```

