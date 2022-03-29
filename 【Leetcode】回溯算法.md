# 【Leetcode】回溯算法



[toc]



## 回溯算法

相关视频：
[带你学透回溯算法（理论篇）| 回溯法精讲！](https://www.bilibili.com/video/BV1cy4y167mM)

代码模板：

```c++
void backtrack(参数) {
    if (终止条件) {
        保存结果;
        return;
    }
    for (循环条件) {
        栈.push(新参数);
        backtrack(新参数);
        栈.pop();
    }
}
```



## 17.电话号码的字母组合

![](D:\Notes\Leetcode\Leetcode.assets\17-1.png)
![](D:\Notes\Leetcode\Leetcode.assets\17-2.png)

我的AC代码：

```c++
class Solution {
public:
	vector<string> v;
	int len;
	unordered_map<char, string> m;
	vector<string> letterCombinations(string digits) {
		m['2'] = "abc";
		m['3'] = "def";
		m['4'] = "ghi";
		m['5'] = "jkl";
		m['6'] = "mno";
		m['7'] = "pqrs";
		m['8'] = "tuv";
		m['9'] = "wxyz";
		len = digits.size();
		if (len != 0) {
			backtrack(digits, "");
		}
		return v;
	}
	void backtrack(string digits, string s) {
		if (s.size() == len) {
			v.push_back(s);
			return;
		}
		string ch = m[digits[s.size()]];
		for (int i = 0; i < ch.size(); i++) {
			backtrack(digits, s + ch[i]);
		}
	}
};
```



## 22.括号生成

![](D:\Notes\Leetcode\Leetcode.assets\22.png)

相关视频：
[Leetcode 22 括号生成 【递归+剪枝， 也可以回溯】](https://www.bilibili.com/video/BV1x5411j7KN)

我的AC代码：

```c++
class Solution {
public:
    int n;
    vector<string> s_list;
    vector<string> generateParenthesis(int n) {
        this->n = n;
        backtrack("(", 1, 0);
        return s_list;
    }
    void backtrack(string s, int ln, int rn) {
        if (ln == n) {
            string res = "";
            for (int i = 1; i <= n - rn; i++) {
                res = res + ")";
            }
            s_list.push_back(s + res);
            return;
        }
        backtrack(s + "(", ln + 1, rn);
        if (ln > rn) {
            backtrack(s + ")", ln, rn + 1);
        }
    }
};
```



## 77. 组合

![](D:\Notes\Leetcode\Leetcode.assets\77-1.png)
![](D:\Notes\Leetcode\Leetcode.assets\77-2.png)

相关视频：
[带你学透回溯算法-组合问题（对应力扣题目：77.组合）| 回溯法精讲！](https://www.bilibili.com/video/BV1ti4y1L7cv)

我的AC代码：
```c++
class Solution {
public:
    int n;
    int k;
    vector<int> s;
    vector<vector<int>> res;
    vector<vector<int>> combine(int n, int k) {
        this->n = n;
        this->k = k;
        backtrack(0, 0);
        return res;
    }
    void backtrack(int idx, int len) {
        if (len == k) {
            res.push_back(s);
            return;
        }
        for (int i = idx + 1; i <= n - k + len + 1; i++) {
            s.push_back(i);
            backtrack(i, len + 1);
            s.pop_back();
        }
    }
};
```