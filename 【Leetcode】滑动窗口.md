# 【Leetcode】滑动窗口



[toc]



|          题目           |                             链接                             | 难度 |
| :---------------------: | :----------------------------------------------------------: | :--: |
|        滑动窗口         | [https://leetcode-cn.com/tag/sliding-window/problemset/](https://leetcode-cn.com/tag/sliding-window/problemset/) | 题库 |
| 3. 无重复字符的最长子串 | [https://leetcode-cn.com/problems/longest-substring-without-repeating-characters/](https://leetcode-cn.com/problems/longest-substring-without-repeating-characters/) | 中等 |
| 30. 串联所有单词的子串  | [https://leetcode-cn.com/problems/substring-with-concatenation-of-all-words/](https://leetcode-cn.com/problems/substring-with-concatenation-of-all-words/) | 困难 |
|  209. 长度最小的子数组  | [https://leetcode-cn.com/problems/minimum-size-subarray-sum/](https://leetcode-cn.com/problems/minimum-size-subarray-sum/) | 中等 |



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



## 30. 串联所有单词的子串

![](D:\Notes\Leetcode\Leetcode.assets\30-1.png)
![](D:\Notes\Leetcode\Leetcode.assets\30-2.png)

相关视频：
[[字幕超清版]leetcode刷题笔记 串联所有单词的子串](https://www.bilibili.com/video/BV1nM4y1V7Wg)

我的AC代码：

```
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

