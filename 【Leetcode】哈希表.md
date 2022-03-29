# 【Leetcode】哈希表



[toc]



## 1. 两数之和

![](D:\Notes\Leetcode\Leetcode.assets\1-1.png)
![](D:\Notes\Leetcode\Leetcode.assets\1-2.png)

相关视频：
[二数之和题解分析](https://www.bilibili.com/video/BV1hV411e7MW)
[二数之和代码解析](https://www.bilibili.com/video/BV1si4y1P7Eg)

我的AC代码：

```c++
class Solution {
public:
	vector<int> twoSum(vector<int>& nums, int target) {
		unordered_map<int, int> m;
		int len = nums.size();
		vector<int> v;
		for (int i = 0; i < len; i++) {
			unordered_map<int, int>::iterator it = m.find(target - nums[i]);
			if (it == m.end()) {
				m.insert(pair<int, int>(nums[i], i));
			}
			else {
				v.push_back(it->second);
				v.push_back(i);
				break;
			}
		}
		return v;
	}
};
```

