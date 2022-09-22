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



## 71. 简化路径

![](D:\Notes\Leetcode\Leetcode.assets\71-1.png)
![](D:\Notes\Leetcode\Leetcode.assets\71-2.png)

相关视频：
[【LeetCode 每日一题】71. 简化路径 | 手写图解版思路 + 代码讲解](https://www.bilibili.com/video/BV1qF411s7Jy)

我的AC代码：

```c++
class Solution {
public:
	string simplifyPath(string path) {
		vector<string> v;
		string res;
		path = path.substr(1);
		if (path.back() != '/') {
			path = path + "/";
		}
		int id = path.find('/');
		while (id != -1) {
			string file = path.substr(0, id);
			path = path.substr(id + 1);
			if (file == "..") {
				if (v.size() != 0) {
					v.pop_back();
				}
			}
			else if (file != "" && file != ".") {
				v.push_back(file);
			}
			id = path.find('/');
		}
		for (vector<string>::iterator it = v.begin(); it != v.end(); it++) {
			res = res + "/" + *it;
		}
		if (v.size() == 0) {
			res = "/";
		}
		return res;
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



## 735. 行星碰撞

![](D:\Notes\Leetcode\Leetcode.assets\735-1.png)
![](D:\Notes\Leetcode\Leetcode.assets\735-2.png)

相关题解：
[行星碰撞](https://leetcode-cn.com/problems/asteroid-collision/solution/xing-xing-peng-zhuang-by-leetcode/)

我的AC代码（解法1）：

```c++
class Solution {
public:
	vector<int> asteroidCollision(vector<int>& asteroids) {
		vector<int> res;
		vector<int> v;
		for (vector<int>::iterator it = asteroids.begin(); it != asteroids.end(); it++) {
			int a = *it;
			if (a > 0) {
				v.push_back(a);
			}
			else {
				while (v.size() != 0 && v.back() < abs(a)) {
					v.pop_back();
				}
				if (v.size() != 0 && v.back() == abs(a)) {
					v.pop_back();
					continue;
				}
				if (v.size() == 0) {
					res.push_back(a);
				}
			}
		}
		for (vector<int>::iterator it = v.begin(); it != v.end(); it++) {
			res.push_back(*it);
		}
		return res;
	}
};
```

我的AC代码（解法2）：

```c++
class Solution {
public:
	vector<int> asteroidCollision(vector<int>& asteroids) {
		vector<int> v1;
		vector<int> v2 = asteroids;
		int len1 = v1.size();
		int len2 = v2.size();
		while (len1 != len2 && len2 > 1) {
			v1 = v2;
			v2 = {};
			len1 = v1.size();
			// first
			if (v1[0] < 0) {
				v2.push_back(v1[0]);
			}
			else { // v1[0] > 0
				if (v1[1] > 0 || v1[1] < 0 && abs(v1[0]) > abs(v1[1])) {
					v2.push_back(v1[0]);
				}
			}
			// middle
			for (int i = 1; i < len1 - 1; i++) {
				if (v1[i] < 0) {
					if (v1[i - 1] > 0 && abs(v1[i]) <= abs(v1[i - 1])) {
						continue;
					}

				}
				else { // v1[i] > 0
					if (v1[i + 1] < 0 && abs(v1[i]) <= abs(v1[i + 1])) {
						continue;
					}
				}
				v2.push_back(v1[i]);
			}
			// last
			if (v1[len1 - 1] > 0) {
				v2.push_back(v1[len1 - 1]);
			}
			else { // v1[len1 - 1] < 0
				if (v1[len1 - 2] < 0 || v1[len1 - 2] > 0 && abs(v1[len1 - 1]) > abs(v1[len1 - 2])) {
					v2.push_back(v1[len1 - 1]);
				}
			}
			len2 = v2.size();
		}
		return v2;
	}
};
```

