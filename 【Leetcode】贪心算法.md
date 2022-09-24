# 【Leetcode】贪心算法



[toc]



## 55. 跳跃游戏

![](D:\Notes\Leetcode\Leetcode.assets\55.png)

相关视频：
[程序员大厂面试必会算法 贪心算法中的经典题目 跳跃游戏 (LeetCode 55)](https://www.bilibili.com/video/BV1Sk4y1C7cD)


我的AC代码（C++）：

```c++
class Solution {
public:
	bool canJump(vector<int>& nums) {
		int len = nums.size();
		int* jump = (int*)malloc(sizeof(int) * len);
		for (int i = 0; i < len; i++) {
			jump[i] = i + nums[i];
		}
		int idx = 0;
		int maxJump = 0;
		while (idx <= maxJump && maxJump < len - 1) {
			if (jump[idx] > maxJump) {
				maxJump = jump[idx];
			}
			idx++;
		}
		
		if (maxJump >= len - 1) {
			return true;
		}
		else {
			return false;
		}
	}
};
```

