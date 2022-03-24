# 【Leetcode】滑动窗口



[toc]



## 3. 无重复字符的最长子串

![](D:\Notes\Leetcode\Leetcode.assets\3-1.png)
![](D:\Notes\Leetcode\Leetcode.assets\3-2.png)

相关视频：
[力扣套路1：滑动窗口](https://www.bilibili.com/video/BV1GZ4y1N7Yu)

我的AC代码：

```c++
class Solution {
public:
	int lengthOfLongestSubstring(string s) {
		int l_idx = 0;
		int r_idx = -1;
		int n = s.size();
		int cnt[256] = { 0 };
		int len = 0;
		int maxLen = 0;

		while (l_idx < n - 1 && r_idx < n - 1) {
			while (cnt[int(s[r_idx + 1])] == 0 && r_idx < n - 1) {
				r_idx += 1;
				cnt[int(s[r_idx])] += 1;
				len += 1;
			}
			if (len > maxLen) {
				maxLen = len;
			}
			r_idx += 1;
			cnt[int(s[r_idx])] += 1;
			len += 1;
			while (cnt[int(s[r_idx])] > 1) {
				cnt[int(s[l_idx])] -= 1;
				l_idx += 1;
				len -= 1;
			}
		}

		if (r_idx == -1 && n != 0) {
			maxLen = n;
		}

		return maxLen;
	}
};
```



## 187. 重复的DNA序列

![](D:\Notes\Leetcode\Leetcode.assets\187.png)

相关视频：
[Leetcode刷题187. 重复的DNA序列 Repeated DNA Sequences](https://www.bilibili.com/video/BV1PQ4y1P7se)

我的AC代码：

```c++
class Solution {
public:
	vector<string> findRepeatedDnaSequences(string s) {
		vector<string> res;
		unordered_map<string, int> m;
		int s_len = s.size();
		int sub_len = 10;
		for (int i = 0; i < s_len - sub_len + 1; i++) {
			string sub = s.substr(i, sub_len);
			unordered_map<string, int>::iterator it = m.find(sub);
			if (it == m.end()) {
				m[sub] = 1;
			}
			else {
				(*it).second++;
			}
		}
		for (unordered_map<string, int>::iterator it = m.begin(); it != m.end(); it++) {
			if ((*it).second > 1) {
				res.push_back((*it).first);
			}
		}
		return res;
	}
};
```



## 209. 长度最小的子数组

![](D:\Notes\Leetcode\Leetcode.assets\209-1.png)
![](D:\Notes\Leetcode\Leetcode.assets\209-2.png)

相关视频：
[LeetCode每日打卡.209.长度最小的子数组](https://www.bilibili.com/video/BV1UA411i77h)

我的AC代码：

```c++
class Solution {
public:
	int minSubArrayLen(int target, vector<int>& nums) {
		int l_idx = 0;
		int r_idx = -1;
		int sum = 0;
		int n = nums.size();
		int len = 0;
		int minLen = n * 2;
		while (r_idx < n - 1 && l_idx < n - 1) {
			while (sum < target && r_idx < n - 1) {
				r_idx += 1;
				sum += nums[r_idx];
				len += 1;
			}
			if (sum >= target && len < minLen) {
				minLen = len;
			}
			while (sum >= target && l_idx < n - 1) {
				sum -= nums[l_idx];
				l_idx += 1;
				len -= 1;
				if (sum >= target && len < minLen) {
					minLen = len;
				}
			}
		}
		if (minLen == n * 2 && sum < target) {
			minLen = 0;
		}
		return minLen;
	}
};
```



## 219. 存在重复元素 II

![](D:\Notes\Leetcode\Leetcode.assets\219-1.png)
![](D:\Notes\Leetcode\Leetcode.assets\219-2.png)

我的AC代码：

```c++
class Solution {
public:
	bool containsNearbyDuplicate(vector<int>& nums, int k) {
		int len = nums.size();
		unordered_map<int, int> m;
		if (k >= len) {
			for (int i = 0; i < len; i++) {
				unordered_map<int, int>::iterator it = m.find(nums[i]);
				if (it == m.end()) {
					m[nums[i]] = 1;
				}
				else {
					(*it).second++;
					if ((*it).second > 1) {
						return true;
					}
				}
			}
		}
		else {
			for (int i = 0; i <= k; i++) {
				unordered_map<int, int>::iterator it = m.find(nums[i]);
				if (it == m.end()) {
					m[nums[i]] = 1;
				}
				else {
					(*it).second++;
					if ((*it).second > 1) {
						return true;
					}
				}
			}
			for (int i = k + 1; i < len; i++) {
				m[nums[i - k - 1]]--;
				unordered_map<int, int>::iterator it = m.find(nums[i]);
				if (it == m.end()) {
					m[nums[i]] = 1;
				}
				else {
					(*it).second++;
					if ((*it).second > 1) {
						return true;
					}
				}
			}
		}
		return false;
	}
};
```



## 220. 存在重复元素 III

![](D:\Notes\Leetcode\Leetcode.assets\220-1.png)
![](D:\Notes\Leetcode\Leetcode.assets\220-2.png)

我的AC代码：

```
```

