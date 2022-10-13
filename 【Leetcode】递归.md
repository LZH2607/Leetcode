# 【Leetcode】递归



[toc]



## 38. 外观数列

![](D:\Notes\Leetcode\Leetcode.assets\38.png)

我的AC代码（Java）：

```java
class Solution {
    public String countAndSay(int n) {
        if (n == 1) {
            return "1";
        }
        char[] arr = countAndSay(n - 1).toCharArray();
        String res = "";
        char ch = arr[0];
        int cnt = 0;
        for (char c : arr) {
            if (c == ch) {
                cnt++;
                continue;
            }
            res = res + cnt + ch;
            ch = c;
            cnt = 1;
        }
        return res + cnt + ch;
    }
}
```



## 1545. 找出第 N 个二进制字符串中的第 K 位

![](D:\Notes\Leetcode\Leetcode.assets\1545.png)

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

