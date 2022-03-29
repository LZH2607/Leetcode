# 【Leetcode】动态规划



[toc]



## 5.最长回文子串

![](D:\Notes\Leetcode\Leetcode.assets\5.png)

相关视频：
[Leetcode 5 最长回文子串 【动态规划解法】](https://www.bilibili.com/video/BV1AA411B7XV)

我的AC代码：

```
```



## 32. 最长有效括号

![](D:\Notes\Leetcode\Leetcode.assets\32-1.png)
![](D:\Notes\Leetcode\Leetcode.assets\32-2.png)

相关视频：
[[LeetCode]. 32 最长有效括号(7分) [动态规划系列]](https://www.bilibili.com/video/BV1VE411t75D)
[LeetCode每日打卡.32.最长有效括号](https://www.bilibili.com/video/BV1Ct4y197M3)

我的AC代码：

```c++
class Solution {
public:
	int longestValidParentheses(string s) {
		s = "  " + s;
		int len = s.size();
		int* dp = (int*)malloc(sizeof(int) * len);
		dp[0] = 0;
		dp[1] = 0;
		int maxDp = 0;
		for (int i = 2; i < len; i++) {
			if (s[i] == '(') {
				dp[i] = 0;
			}
			else {
				if (s[i - dp[i - 1] - 1] == '(') {
					dp[i] = 2 + dp[i - 1] + dp[i - dp[i - 1] - 2];
				}
				else {
					dp[i] = 0;
				}
				if (dp[i] > maxDp) {
					maxDp = dp[i];
				}
			}
		}
		return maxDp;
	}
};
```


