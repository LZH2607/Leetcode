# 【Leetcode】栈



[toc]



## 20. 有效的括号

![](D:\Notes\Leetcode\Leetcode.assets\20-1.png)
![](D:\Notes\Leetcode\Leetcode.assets\20-2.png)

我的AC代码：

```c++
class Solution {
public:
	bool isValid(string s) {
		int len = s.size();
		bool flag = true;
		vector<char> v;
		for (int i = 0; i < len && flag; i++) {
			char c = s[i];
			switch (c)
			{
			case ')':
				if (v.size() == 0) {
					flag = false;
				}
				else if (v.back() != '(') {
					flag = false;
				}
				else {
					v.pop_back();
				}
				break;
			case ']':
				if (v.size() == 0) {
					flag = false;
				}
				else if (v.back() != '[') {
					flag = false;
				}
				else {
					v.pop_back();
				}
				break;
			case '}':
				if (v.size() == 0) {
					flag = false;
				}
				else if (v.back() != '{') {
					flag = false;
				}
				else {
					v.pop_back();
				}
				break;
			default:
				v.push_back(c);
			}
		}
		if (len == 1 || v.size() > 0) {
			flag = false;
		}
		return flag;
	}
};
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



## 150. 逆波兰表达式求值

![](D:\Notes\Leetcode\Leetcode.assets\150-1.png)
![](D:\Notes\Leetcode\Leetcode.assets\150-2.png)
![](D:\Notes\Leetcode\Leetcode.assets\150-3.png)

我的AC代码：

```c++
class Solution {
public:
	int evalRPN(vector<string>& tokens) {
		vector<int> v;
		int len = tokens.size();
		for (int i = 0; i < len; i++) {
			if (tokens[i] == "+") {
				int b = v.back();
				v.pop_back();

				int a = v.back();
				v.pop_back();

				int c = a + b;
				v.push_back(c);

			}
			else if (tokens[i] == "-") {
				int b = v.back();
				v.pop_back();

				int a = v.back();
				v.pop_back();

				int c = a - b;
				v.push_back(c);
			}
			else if (tokens[i] == "*") {
				int b = v.back();
				v.pop_back();

				int a = v.back();
				v.pop_back();

				int c = a * b;
				v.push_back(c);
			}
			else if (tokens[i] == "/") {
				int b = v.back();
				v.pop_back();

				int a = v.back();
				v.pop_back();

				int c = a / b;
				v.push_back(c);
			}
			else {
				int x = atoi(tokens[i].c_str());
				v.push_back(x);
			}
		}
		return v[0];
	}
};
```


