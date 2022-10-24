# 【Leetcode】技巧



[toc]



## 334. 递增的三元子序列

![](D:\Notes\Leetcode\Leetcode.assets\334.png)

相关视频：
[LeetCode 每日一题 Daily Challenge 334 Increasing Triplet Subsequence](https://www.youtube.com/watch?v=xPKk7Zxyxe4)

我的AC代码（Java）：

```java
class Solution {
    public boolean increasingTriplet(int[] nums) {
        int min = Integer.MAX_VALUE;
        int mid = Integer.MAX_VALUE;
        for (int num : nums) {
            if (num <= min) {
                min = num;
            } else if (num <= mid) {
                mid = num;
            } else {  // num > mid
                return true;
            }
        }
        return false;
    }
}
```

