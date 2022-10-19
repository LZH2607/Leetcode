# 【Leetcode】排列组合



[toc]



相关笔记：【Leetcode】回溯算法



## 31. 下一个排列

![](D:\Notes\Leetcode\Leetcode.assets\31.png)

相关文章：

![](D:\Notes\Leetcode\Leetcode.assets\31-solution.png)

我的AC代码（Java）：

```java
class Solution {
    public void nextPermutation(int[] nums) {
        int len = nums.length;
        boolean flag = false;
        for (int i = len - 1; i > 0; i--) {
            if (nums[i - 1] < nums[i]) {
                for (int j = len - 1; j > i - 1; j--) {
                    if (nums[j] > nums[i - 1]) {
                        int temp = nums[j];
                        nums[j] = nums[i - 1];
                        nums[i - 1] = temp;
                        break;
                    }
                }
                Arrays.sort(nums, i, len);
                flag = true;
                break;
            }
        }
        if (!flag) {
            Arrays.sort(nums);
        }
    }
}
```



## 60. 排列序列

![](D:\Notes\Leetcode\Leetcode.assets\60.png)

我的AC代码（Java）：

```java
class Solution {
    public String getPermutation(int n, int k) {
        List<String> l = new ArrayList<>();
        for (int i = 1; i <= n; i++) {
            l.add(i + "");
        }
        String res = "";
        n--;
        k--;
        int factorial = 1;
        for (int i = 1; i <= n; i++) {
            factorial *= i;
        }
        while (n > 0) {
            int idx = k / factorial;
            res += l.remove(idx);
            k -= idx * factorial;
            factorial /= n;
            n--;
        }
        res += l.remove(0);
        return res;
    }
}
```

