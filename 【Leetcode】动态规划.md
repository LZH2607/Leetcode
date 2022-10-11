# 【Leetcode】动态规划



[toc]



## 5.最长回文子串

![](D:\Notes\Leetcode\Leetcode.assets\5.png)

相关视频：
[Leetcode 5 最长回文子串 【动态规划解法】](https://www.bilibili.com/video/BV1AA411B7XV)

我的AC代码（C++）：

```c++
class Solution {
public:
	string longestPalindrome(string s) {
		int len = s.size();
		int subLen = 1;
		string sub = s.substr(0, 1);
		bool** dp = (bool**)malloc(sizeof(bool*) * len);
		for (int i = 0; i < len; i++) {
			dp[i] = (bool*)malloc(sizeof(bool) * len);
		}
		for (int i = 0; i < len; i++) {
			dp[i][i] = true;
			if (i < len - 1) {
				if (s[i] == s[i + 1]) {
					dp[i][i + 1] = true;
					subLen = 2;
					sub = s.substr(i, subLen);
				}
				else {
					dp[i][i + 1] = false;
				}
			}
		}
		for (int j = 2; j < len; j++) {
			for (int i = 0; i < len - j; i++) {
				if (s[i] != s[i + j]) {
					dp[i][i + j] = false;
				}
				else {
					dp[i][i + j] = dp[i + 1][i + j - 1];
					if (dp[i][i + j] && j + 1 > subLen) {
						subLen = j + 1;
						sub = s.substr(i, j + 1);
					}
				}
			}
		}
		return sub;
	}
};
```



## 32. 最长有效括号

![](D:\Notes\Leetcode\Leetcode.assets\32.png)

相关视频：
[[LeetCode]. 32 最长有效括号(7分) [动态规划系列]](https://www.bilibili.com/video/BV1VE411t75D)
[LeetCode每日打卡.32.最长有效括号](https://www.bilibili.com/video/BV1Ct4y197M3)

我的AC代码（C++）：

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



## 62. 不同路径

![](D:\Notes\Leetcode\Leetcode.assets\62.png)

相关视频：
[力扣 Leetcode 62.  不同路径 Python算法 Leetcode 算法刷题 第62题 例子阐述 时间74% 极简代码 两种解法 清晰易懂 极简](https://www.bilibili.com/video/BV1zp4y1i7Zz?spm_id_from=333.851.header_right.history_list.click)

我的AC代码（C++）：

```c++
class Solution {
public:
	int dp[100][100];
	int uniquePaths(int m, int n) {
		for (int j = 0; j < n; j++) {
			dp[0][j] = 1;
		}
		for (int i = 0; i < m; i++) {
			dp[i][0] = 1;
		}
		for (int i = 1; i < m; i++) {
			for (int j = 1; j < n; j++) {
				dp[i][j] = dp[i][j - 1] + dp[i - 1][j];
			}
		}
		return dp[m - 1][n - 1];
	}
};
```



## 63. 不同路径 II

![](D:\Notes\Leetcode\Leetcode.assets\63.png)

相关视频：
[力扣 Leetcode 63.  不同路径II Python算法 Leetcode 算法刷题 第63题 例子阐述 时间58% 极简代码 思路清晰易懂](https://www.bilibili.com/video/BV1gz4y1Q7Yu)

我的AC代码（C++）：

```c++
class Solution {
public:
	int dp[100][100];
	int uniquePathsWithObstacles(vector<vector<int>>& obstacleGrid) {
		int m = obstacleGrid.size();
		int n = obstacleGrid[0].size();
		if (obstacleGrid[0][0] == 1) {
			dp[0][0] = 0;
		}
		else {
			dp[0][0] = 1;
		}
		
		for (int j = 1; j < n; j++) {
			if (obstacleGrid[0][j] == 1) {
				dp[0][j] = 0;
			}
			else {
				dp[0][j] = dp[0][j - 1];
			}
		}
		for (int i = 1; i < m; i++) {
			if (obstacleGrid[i][0] == 1) {
				dp[i][0] = 0;
			}
			else {
				dp[i][0] = dp[i - 1][0];
			}
		}
		for (int i = 1; i < m; i++) {
			for (int j = 1; j < n; j++) {
				if (obstacleGrid[i][j] == 1) {
					dp[i][j] = 0;
				}
				else {
					dp[i][j] = dp[i][j - 1] + dp[i - 1][j];
				}
			}
		}
		return dp[m - 1][n - 1];
	}
};
```

