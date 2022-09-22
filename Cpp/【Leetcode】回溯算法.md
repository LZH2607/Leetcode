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



## 37. 解数独

![](D:\Notes\Leetcode\Leetcode.assets\37-1.png)
![](D:\Notes\Leetcode\Leetcode.assets\37-2.png)
![](D:\Notes\Leetcode\Leetcode.assets\37-3.png)
![](D:\Notes\Leetcode\Leetcode.assets\37-4.png)

相关视频：
[【算法演示】回溯法求解数独，leetcode37题](https://www.bilibili.com/video/BV16U4y1E72g)

我的AC代码：

```c++
class Solution {
public:
	bool cntRow[9][10];
	bool cntCol[9][10];
	bool cntSubBox[9][10];
	void solveSudoku(vector<vector<char>>& board) {
		initCnt(board);
		backtrack(board, 0, 0);
	}
	void initCnt(vector<vector<char>>& board) {
		for (int i = 0; i < 9; i++) {
			for (int j = 0; j < 10; j++) {
				cntRow[i][j] = false;
				cntCol[i][j] = false;
				cntSubBox[i][j] = false;
			}
		}
		for (int i = 0; i < 9; i++) {
			for (int j = 0; j < 9; j++) {
				if (board[i][j] != '.') {
					int d = (int)board[i][j] - (int)'0';
					int b = (i / 3) * 3 + j / 3;
					cntRow[i][d] = true;
					cntCol[j][d] = true;
					cntSubBox[b][d] = true;
				}
				
			}
		}
	}
	bool backtrack(vector<vector<char>>& board, int i, int j) {
		if (board[i][j] != '.') {
			if (i == 8 && j == 8) {
				return true;
			}
			else if (j < 8) {
				return backtrack(board, i, j + 1);
			}
			else {
				return backtrack(board, i + 1, 0);
			}
		}
		else {
			vector<int> ds = findDigits(i, j);
			if (ds.size() != 0) {
				for (vector<int>::iterator it = ds.begin(); it != ds.end(); it++) {
					int d = *it;
					setDigit(board, i, j, d);
					if (i == 8 && j == 8) {
						return true;
					}
					else if (j < 8) {
						if (backtrack(board, i, j + 1)) {
							return true;
						}
					}
					else {
						if (backtrack(board, i + 1, 0)) {
							return true;
						}
					}
					resetDigit(board, i, j, d);
				}
			}
			return false;
		}
	}
	vector<int> findDigits(int i, int j) {
		vector<int> ds;
		int b = (i / 3) * 3 + j / 3;
		for (int d = 1; d < 10; d++) {
			if (!cntRow[i][d] && !cntCol[j][d] && !cntSubBox[b][d]) {
				ds.push_back(d);
			}
		}
		return ds;
	}
	void setDigit(vector<vector<char>>& board, int i, int j, int d) {
		board[i][j] = (char)(d + (int)'0');
		int b = (i / 3) * 3 + j / 3;
		cntRow[i][d] = true;
		cntCol[j][d] = true;
		cntSubBox[b][d] = true;
	}
	void resetDigit(vector<vector<char>>& board, int i, int j, int d) {
		board[i][j] = '.';
		int b = (i / 3) * 3 + j / 3;
		cntRow[i][d] = false;
		cntCol[j][d] = false;
		cntSubBox[b][d] = false;
	}
};
```



## 39. 组合总和

![](D:\Notes\Leetcode\Leetcode.assets\39-1.png)
![](D:\Notes\Leetcode\Leetcode.assets\39-2.png)

相关视频：
[带你学透回溯算法-组合总和（对应「leetcode」力扣题目：39.组合总和）| 回溯法精讲！](https://www.bilibili.com/video/BV1KT4y1M7HJ)

我的AC代码：

```c++
class Solution {
public:
	vector<vector<int>> vv;
	vector<vector<int>> combinationSum(vector<int>& candidates, int target) {
		sort(candidates.begin(), candidates.end());
		vector<int> v;
		backtrack(candidates, v, target);
		return vv;
	}
	void backtrack(vector<int>& candidates, vector<int>& v, int res) {
		if (res == 0) {
			vector<int> t = v;
			sort(t.begin(), t.end());
			if (find(vv.begin(), vv.end(), t) == vv.end()) {
				vv.push_back(t);
			}
			return;
		}
		int len = candidates.size();
		for (int i = 0; i < len; i++) {
			if (candidates[i] <= res) {
				v.push_back(candidates[i]);
				backtrack(candidates, v, res - candidates[i]);
				v.pop_back();
			}
		}
		return;
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