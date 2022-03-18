# 【Leetcode】双指针



[toc]



|         题目         |                             链接                             | 难度 |
| :------------------: | :----------------------------------------------------------: | :--: |
|        双指针        | [https://leetcode-cn.com/tag/two-pointers/problemset/](https://leetcode-cn.com/tag/two-pointers/problemset/) | 题库 |
|  11. 盛最多水的容器  | [https://leetcode-cn.com/problems/container-with-most-water/](https://leetcode-cn.com/problems/container-with-most-water/) | 中等 |
|     15. 三数之和     | [https://leetcode-cn.com/problems/3sum/](https://leetcode-cn.com/problems/3sum/) | 中等 |
| 16. 最接近的三数之和 | [https://leetcode-cn.com/problems/3sum-closest/](https://leetcode-cn.com/problems/3sum-closest/) | 中等 |
|     18. 四数之和     | [https://leetcode-cn.com/problems/4sum/](https://leetcode-cn.com/problems/4sum/) | 中等 |



## 11. 盛最多水的容器

![](D:\Notes\Leetcode\Leetcode.assets\11-1.png)
![](D:\Notes\Leetcode\Leetcode.assets\11-2.png)
![](D:\Notes\Leetcode\Leetcode.assets\11-3.png)

相关视频：
[五分钟力扣 Leetcode 第11题 盛最多水的容器  Python入门算法刷题 解法 80%](https://www.bilibili.com/video/BV1uc411h7XA)

我的AC代码：

```c++
class Solution {
public:
	int maxArea(vector<int>& height) {
		int l_idx = 0;
		int r_idx = height.size() - 1;
		int area = min(height[l_idx], height[r_idx]) * (r_idx - l_idx);
		int maxArea = area;
		while (l_idx != r_idx) {
			if (height[l_idx] < height[r_idx]) {
				l_idx = l_idx + 1;
				area = min(height[l_idx], height[r_idx]) * (r_idx - l_idx);
				if (area > maxArea) {
					maxArea = area;
				}
			}
			else {
				r_idx = r_idx - 1;
				area = min(height[l_idx], height[r_idx]) * (r_idx - l_idx);
				if (area > maxArea) {
					maxArea = area;
				}
			}
		}
		return maxArea;
	}
};
```



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
				res.push_back(com);
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



## 16. 最接近的三数之和

![](D:\Notes\Leetcode\Leetcode.assets\16.png)

我的AC代码：

```c++
class Solution {
public:
	int len;
	int closestSum;
	int closestDiff;
	int threeSumClosest(vector<int>& nums, int target) {
		sort(nums.begin(), nums.end());
		len = nums.size();
		closestSum = 20000;
		closestDiff = abs(target - closestSum);
		int i = 0;
		while (i < len - 2) {
			int l_idx = i + 1;
			int r_idx = len - 1;
			find(nums, target, i, l_idx, r_idx);
			if (closestSum == target) {
				break;
			}
			while (nums[i] == nums[i + 1] && i < len - 2) {
				i += 1;
			}
			i += 1;
		}
		return closestSum;
	}
	void find(vector<int>& nums, int target, int i, int l_idx, int r_idx) {
		while (l_idx < r_idx) {
			int sum = nums[i] + nums[l_idx] + nums[r_idx];
			int diff = abs(target - sum);
			if (diff < closestDiff) {
				closestSum = sum;
				closestDiff = diff;
			}
			if (sum == target) {
				return;
			}
			else if (sum < target) {
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



## 18. 四数之和

![](D:\Notes\Leetcode\Leetcode.assets\18-1.png)
![](D:\Notes\Leetcode\Leetcode.assets\18-2.png)

相关视频：
[【忍者算法】LeetCode 18 四数之和](https://www.bilibili.com/video/BV1r341147JQ)

我的AC代码：

```c++
class Solution {
public:
	vector<vector<int>> res;
	int len;
	vector<vector<int>> fourSum(vector<int>& nums, int target) {
		sort(nums.begin(), nums.end());
		len = nums.size();
		int i = 0;
		while (i < len - 3) {
			int j = i + 1;
			while (j < len - 2) {
				int l_idx = j + 1;
				int r_idx = len - 1;
				find(nums, i, j, l_idx, r_idx, target);
				while (nums[j] == nums[j + 1] && j < len - 2) {
					j += 1;
				}
				j += 1;
			}
			while (nums[i] == nums[i + 1] && i < len - 3) {
				i += 1;
			}
			i += 1;
		}
		return res;
	}
	void find(vector<int>& nums, int i, int j, int l_idx, int r_idx, int target) {
		while (j < l_idx && l_idx < r_idx) {
			long long sum = (long long)nums[i] + (long long)nums[j] + (long long)nums[l_idx] + (long long)nums[r_idx];
			if (sum == (long long)target) {
				vector<int> com = { nums[i], nums[j], nums[l_idx], nums[r_idx] };
				res.push_back(com);
				while (nums[l_idx] == nums[l_idx + 1] && l_idx + 1 < r_idx) {
					l_idx += 1;
				}
				l_idx += 1;
				while (nums[r_idx - 1] == nums[r_idx] && r_idx - 1 > l_idx) {
					r_idx -= 1;
				}
				r_idx -= 1;
			}
			else if (sum < (long long)target) {
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



