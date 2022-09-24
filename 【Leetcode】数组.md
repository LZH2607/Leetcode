# 【Leetcode】数组



[toc]



## 665. 非递减数列

![](D:\Notes\Leetcode\Leetcode.assets\665.png)

相关视频：
[665. Non-decreasing Array 思路就一个 0290](https://www.youtube.com/watch?v=oURS2fk4T-w)

我的AC代码（C++）：

```c++
class Solution {
public:
	bool checkPossibility(vector<int>& nums) {
		int len = nums.size();
		if (len >= 3) {
			int cnt = 0;
			if (nums[0] > nums[1]) {
				nums[0] = nums[1];
				cnt++;
			}
			for (int i = 0; i < len - 2; i++) {
				if (nums[i + 1] > nums[i + 2]) {
					if (nums[i] > nums[i + 2]) {
						nums[i + 2] = nums[i + 1];
						cnt++;
						if (cnt > 1) {
							return false;
						}
					}
					else {
						nums[i + 1] = nums[i + 2];
						cnt++;
						if (cnt > 1) {
							return false;
						}
					}
				}
			}
		}
		return true;		
	}
};
```

