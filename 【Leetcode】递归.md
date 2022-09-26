# 【Leetcode】递归



[toc]



## 1545. 找出第 N 个二进制字符串中的第 K 位

![](D:\Notes\Leetcode\Leetcode.assets\1545-1.png)
![](D:\Notes\Leetcode\Leetcode.assets\1545-2.png)

我的AC代码（Java）：

```java
class Solution {
    public char findKthBit(int n, int k) {
        if (n == 1) {
            return '0';
        }
        if (k < 1 << (n - 1)) {  // k < 2 ^ (n - 1)
            return findKthBit(n - 1, k);
        } else if (k == 1 << (n - 1)) {  // k == 2 ^ (n - 1)
            return '1';
        }  // k > 2 ^ (n - 1)
        char c = findKthBit(n - 1, (1 << n) - k);  // findKthBit(n - 1, 2 ^ n - k)
        if (c == '1') {
            return '0';
        }
        return '1';
    }
}
```

