# 【Leetcode】规则



[toc]



## 14. 最长公共前缀

![](D:\Notes\Leetcode\Leetcode.assets\14.png)

我的AC代码（C++）：

```c++
class Solution {
public:
	string longestCommonPrefix(vector<string>& strs) {
		int n = strs.size();
		int minLen = 200;
		for (int i = 0; i < n; i++) {
			if (strs[i].size() < minLen) {
				minLen = strs[i].size();
			}
		}
		string prefix;
		int len;
		for (len = 0; len < minLen; len++) {
			char c = strs[0][len];
			bool flag = false;
			for (int i = 0; i < n; i++) {
				if (strs[i][len] != c) {
					flag = true;
					break;
				}
			}
			if (flag) {
				break;
			}
		}
		if (len == 0) {
			prefix = "";
		}
		else {
			prefix = strs[0].substr(0, len);
		}
		return prefix;
	}
};
```



## 36. 有效的数独

![](D:\Notes\Leetcode\Leetcode.assets\36-1.png)
![](D:\Notes\Leetcode\Leetcode.assets\36-2.png)
![](D:\Notes\Leetcode\Leetcode.assets\36-3.png)

我的AC代码（C++）：

```c++
class Solution {
public:
	bool isValidSudoku(vector<vector<char>>& board) {
		for (int i = 0; i < 9; i++) {
			if (!checkRow(board, i)) {
				return false;
			}
		}
		for (int j = 0; j < 9; j++) {
			if (!checkCol(board, j)) {
				return false;
			}
		}
		for (int i = 0; i < 9; i += 3) {
			for (int j = 0; j < 9; j += 3) {
				if (!checkSubBox(board, i, j)) {
					return false;
				}
			}
		}
		return true;
	}
	bool checkRow(vector<vector<char>>& board, int i) {
		bool cnt[10] = { false };
		for (int j = 0; j < 9; j++) {
			if (board[i][j] != '.') {
				int idx = (int)board[i][j] - (int)'0';
				if (cnt[idx]) {
					return false;
				}
				else {
					cnt[idx] = true;
				}
			}
		}
		return true;
	}
	bool checkCol(vector<vector<char>>& board, int j) {
		bool cnt[10] = { false };
		for (int i = 0; i < 9; i++) {
			if (board[i][j] != '.') {
				int idx = (int)board[i][j] - (int)'0';
				if (cnt[idx]) {
					return false;
				}
				else {
					cnt[idx] = true;
				}
			}
		}
		return true;
	}
	bool checkSubBox(vector<vector<char>>& board, int r, int c) {
		bool cnt[10] = { false };
		for (int i = r; i < r + 3; i++) {
			for (int j = c; j < c + 3; j++) {
				if (board[i][j] != '.') {
					int idx = (int)board[i][j] - (int)'0';
					if (cnt[idx]) {
						return false;
					}
					else {
						cnt[idx] = true;
					}
				}
			}
		}
		return true;
	}
};
```

我的AC代码（Java）：

```java
class Solution {
	public boolean isValidSudoku(char[][] board) {
		for (int i = 0; i < 9; i++) {
			if (!checkRow(board, i)) {
				return false;
			}
		}
		for (int j = 0; j < 9; j++) {
			if (!checkCol(board, j)) {
				return false;
			}
		}
		for (int i = 0; i < 9; i += 3) {
			for (int j = 0; j < 9; j += 3) {
				if (!checkSubBox(board, i, j)) {
					return false;
				}
			}
		}
		return true;
	}

	private boolean checkRow(char[][] board, int i) {
		boolean cnt[] = new boolean[10];
		for (int j = 0; j < 9; j++) {
			if (board[i][j] != '.') {
				int idx = (int) board[i][j] - (int) '0';
				if (cnt[idx]) {
					return false;
				} else {
					cnt[idx] = true;
				}
			}
		}
		return true;
	}

	private boolean checkCol(char[][] board, int j) {
		boolean cnt[] = new boolean[10];
		for (int i = 0; i < 9; i++) {
			if (board[i][j] != '.') {
				int idx = (int) board[i][j] - (int) '0';
				if (cnt[idx]) {
					return false;
				} else {
					cnt[idx] = true;
				}
			}
		}
		return true;
	}

	private boolean checkSubBox(char[][] board, int r, int c) {
		boolean cnt[] = new boolean[10];
		for (int i = r; i < r + 3; i++) {
			for (int j = c; j < c + 3; j++) {
				if (board[i][j] != '.') {
					int idx = (int) board[i][j] - (int) '0';
					if (cnt[idx]) {
						return false;
					} else {
						cnt[idx] = true;
					}
				}
			}
		}
		return true;
	}
}
```



## 1122. 数组的相对排序

![](D:\Notes\Leetcode\Leetcode.assets\1122.png)

我的AC代码（Java）：

```java
class Solution {
    public int[] relativeSortArray(int[] arr1, int[] arr2) {
        HashMap<Integer, Integer> m = new HashMap<>();
        ArrayList<Integer> l = new ArrayList<>();
        ArrayList<Integer> r = new ArrayList<>();
        int[] arr3 = new int[arr1.length];
        for (int i : arr2) {
            m.put(i, 0);
        }
        for (int i : arr1) {
            if (m.containsKey(i)) {
                m.put(i, m.get(i) + 1);
            } else {
                l.add(i);
            }
        }
        Collections.sort(l);
        for (int n : arr2) {
            for (int i = 0; i < m.get(n); i++) {
                r.add(n);
            }
        }
        r.addAll(l);
        for (int i = 0; i < r.size(); i++) {
            arr3[i] = r.get(i);
        }
        return arr3;
    }
}
```

