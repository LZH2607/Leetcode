# 【Leetcode】双指针



[toc]



|     题目     |                             链接                             | 难度 |
| :----------: | :----------------------------------------------------------: | :--: |
|    双指针    | [https://leetcode-cn.com/tag/two-pointers/problemset/](https://leetcode-cn.com/tag/two-pointers/problemset/) | 题库 |
| 15. 三数之和 | [https://leetcode-cn.com/problems/3sum/](https://leetcode-cn.com/problems/3sum/) | 中等 |
|              |                                                              |      |



## 15. 三数之和

![](D:\Notes\Leetcode\Leetcode.assets\15-1.png)
![](D:\Notes\Leetcode\Leetcode.assets\15-2.png)

相关视频：
[三数之和题目解析](https://www.bilibili.com/video/BV1kU4y1a7Pj)

我的AC代码：

```c++
class Solution {
public:
	vector<vector<int>> res;
	set<vector<int>> s;
	int len;
	vector<vector<int>> threeSum(vector<int>& nums) {
		sort(nums.begin(), nums.end());
		len = nums.size();
		int i = 0;
		while (i < len - 2) {
			int l_idx = i + 1;
			int r_idx = len - 1;
			find(nums, i, l_idx, r_idx);
			while (nums[i] == nums[i + 1] && i < len - 2) {
				i += 1;
			}
			i += 1;
		}
		return res;
	}
	void find(vector<int>& nums, int i, int l_idx, int r_idx) {
		while (l_idx < r_idx) {
			int sum = nums[i] + nums[l_idx] + nums[r_idx];
			if (sum == 0) {
				vector<int> com = { nums[i], nums[l_idx], nums[r_idx] };
				sort(com.begin(), com.end());
				if (s.find(com) == s.end()) {
					s.insert(com);
					res.push_back(com);
				}
				while (nums[l_idx] == nums[l_idx + 1] && l_idx + 1 < r_idx) {
					l_idx += 1;
				}
				l_idx += 1;
				while (nums[r_idx - 1] == nums[r_idx] && r_idx - 1 > l_idx) {
					r_idx -= 1;
				}
				r_idx -= 1;
			}
			else if (sum < 0) {
				while (nums[l_idx] == nums[l_idx + 1] && l_idx + 1 < r_idx) {
					l_idx += 1;
				}
				l_idx += 1;
			}
			else {
				while (nums[r_idx - 1] == nums[r_idx] && r_idx - 1 > l_idx) {
					r_idx -= 1;
				}
				r_idx -= 1;
			}
		}
	}
};
```

