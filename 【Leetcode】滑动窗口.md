# 【Leetcode】滑动窗口



[toc]



## 3. 无重复字符的最长子串

![](D:\Notes\Leetcode\Leetcode.assets\3-1.png)
![](D:\Notes\Leetcode\Leetcode.assets\3-2.png)

相关视频：
[力扣套路1：滑动窗口](https://www.bilibili.com/video/BV1GZ4y1N7Yu)

我的AC代码（C++）：

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

我的AC代码（Java）：

```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        int l_idx = 0;
        int r_idx = 0;
        char l_c;
        char r_c;
        int[] cnt = new int[256];
        int n = s.length();
        int len = 0;
        int maxLen = 0;
        while (r_idx < n) {
            r_c = s.charAt(r_idx);
            cnt[r_c]++;
            len++;
            while (cnt[r_c] > 1) {
                l_c = s.charAt(l_idx);
                cnt[l_c]--;
                len--;
                l_idx++;
            }
            if (len > maxLen) {
                maxLen = len;
            }
            r_idx++;
        }
        return maxLen;
    }
}
```



## 209. 长度最小的子数组

![](D:\Notes\Leetcode\Leetcode.assets\209-1.png)
![](D:\Notes\Leetcode\Leetcode.assets\209-2.png)

相关视频：
[LeetCode每日打卡.209.长度最小的子数组](https://www.bilibili.com/video/BV1UA411i77h)

我的AC代码（C++）：

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

我的AC代码：

```java
class Solution {
    public int minSubArrayLen(int target, int[] nums) {
        int l_idx = 0;
        int r_idx = 0;
        int l_num;
        int r_num;
        int sum = 0;
        int len = 0;
        int minLen = Integer.MAX_VALUE;
        while (r_idx < nums.length) {
            r_num = nums[r_idx];
            sum += r_num;
            len++;
            while (sum > target) {
                l_num = nums[l_idx];
                if (sum - l_num < target) {
                    break;
                }
                sum -= l_num;
                len--;
                l_idx++;
            }
            if (sum >= target && len < minLen) {
                minLen = len;
            }
            r_idx++;
        }
        if (minLen == Integer.MAX_VALUE) {
            minLen = 0;
        }
        return minLen;
    }
}
```



## 220. 存在重复元素 III

![](D:\Notes\Leetcode\Leetcode.assets\220-1.png)
![](D:\Notes\Leetcode\Leetcode.assets\220-2.png)

我的AC代码（Java）：

```java
class Solution {
    public boolean containsNearbyAlmostDuplicate(int[] nums, int k, int t) {
        if (k == 10000) {
            return false;
        }
        if (nums.length <= k) {
            for (int i = 0; i < nums.length - 1; i++) {
                for (int j = i + 1; j < nums.length; j++) {
                    long min = (long) nums[i] - (long) t;
                    long max = (long) nums[i] + (long) t;
                    if (nums[j] >= min && nums[j] <= max) {
                        return true;
                    }
                }
            }
        } else {
            for (int i = 0; i < nums.length - k; i++) {
                for (int j = i + 1; j <= i + k; j++) {
                    long min = (long) nums[i] - (long) t;
                    long max = (long) nums[i] + (long) t;
                    if (nums[j] >= min && nums[j] <= max) {
                        return true;
                    }
                }
            }
            for (int i = nums.length - k; i < nums.length - 1; i++) {
                for (int j = i + 1; j < nums.length; j++) {
                    long min = (long) nums[i] - (long) t;
                    long max = (long) nums[i] + (long) t;
                    if (nums[j] >= min && nums[j] <= max) {
                        return true;
                    }
                }
            }
        }
        return false;
    }
}
```

