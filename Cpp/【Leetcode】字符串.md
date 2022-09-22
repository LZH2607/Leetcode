# 【Leetcode】字符串



[toc]



## 14. 最长公共前缀

![](D:\Notes\Leetcode\Leetcode.assets\14.png)

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

