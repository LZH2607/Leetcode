# 【Leetcode】双指针



[toc]



相关文章：
[算法一招鲜——双指针问题](https://zhuanlan.zhihu.com/p/71643340)

双指针：
	对撞指针
	快慢指针



## 11. 盛最多水的容器

![](D:\Notes\Leetcode\Leetcode.assets\11.png)

相关视频：
[五分钟力扣 Leetcode 第11题 盛最多水的容器  Python入门算法刷题 解法 80%](https://www.bilibili.com/video/BV1uc411h7XA)

我的AC代码（C++）：

```c++
class Solution {
public:
	int maxArea(vector<int>& height) {
		int l_idx = 0;
		int r_idx = height.size() - 1;
		int maxArea = 0;
		while (l_idx < r_idx) {
			int l_h = height[l_idx];
			int r_h = height[r_idx];
			int area = min(l_h, r_h) * (r_idx - l_idx);
			if (maxArea < area) {
				maxArea = area;
			}
			if (l_h > r_h) {
				r_idx--;
			}
			else {
				l_idx++;
			}
		}
		return maxArea;
	}
};
```

我的AC代码（Java）：

```java
class Solution {
    public int maxArea(int[] height) {
        int l_idx = 0;
        int r_idx = height.length - 1;
        int maxArea = 0;
        while (l_idx < r_idx) {
            int l_h = height[l_idx];
            int r_h = height[r_idx];
            int area = Math.min(l_h, r_h) * (r_idx - l_idx);
            if (maxArea < area) {
                maxArea = area;
            }
            if (l_h > r_h) {
                r_idx--;
            } else {
                l_idx++;
            }
        }
        return maxArea;
    }
}
```



## 15. 三数之和

![](D:\Notes\Leetcode\Leetcode.assets\15.png)

相关视频：
[三数之和题目解析](https://www.bilibili.com/video/BV1kU4y1a7Pj)

我的AC代码（C++）：

```c++
class Solution {
public:
	vector<vector<int>> vv;
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
				i++;
			}
			i++;
		}
		return vv;
	}
	void find(vector<int>& nums, int i, int l_idx, int r_idx) {
		while (l_idx < r_idx) {
			int sum = nums[i] + nums[l_idx] + nums[r_idx];
			if (sum == 0) {
				vector<int> v = { nums[i], nums[l_idx], nums[r_idx] };
				vv.push_back(v);
				while (nums[l_idx] == nums[l_idx + 1] && l_idx < len - 2) {
					l_idx++;
				}
				l_idx++;
				while (nums[r_idx] == nums[r_idx - 1] && r_idx > i + 2) {
					r_idx--;
				}
				r_idx--;
			}
			else if (sum > 0) {
				while (nums[r_idx] == nums[r_idx - 1] && r_idx > i + 2) {
					r_idx--;
				}
				r_idx--;
			}
			else {  // sum < 0
				while (nums[l_idx] == nums[l_idx + 1] && l_idx < len - 2) {
					l_idx++;
				}
				l_idx++;
			}
		}
	}
};
```

我的AC代码（Java）：

```java
class Solution {
    List<List<Integer>> ll = new ArrayList<>();
    int len;

    public List<List<Integer>> threeSum(int[] nums) {
        Arrays.sort(nums);
        len = nums.length;
        int i = 0;
        while (i < len - 2) {
            int l_idx = i + 1;
            int r_idx = len - 1;
            find(nums, i, l_idx, r_idx);
            while (nums[i] == nums[i + 1] && i < len - 2) {
                i++;
            }
            i++;
        }
        return ll;
    }

    void find(int[] nums, int i, int l_idx, int r_idx) {
        while (l_idx < r_idx) {
            int sum = nums[i] + nums[l_idx] + nums[r_idx];
            if (sum == 0) {
                List<Integer> l = new ArrayList<>();
                l.add(nums[i]);
                l.add(nums[l_idx]);
                l.add(nums[r_idx]);
                ll.add(l);
                while (nums[l_idx] == nums[l_idx + 1] && l_idx < len - 2) {
                    l_idx++;
                }
                l_idx++;
                while (nums[r_idx] == nums[r_idx - 1] && r_idx > i + 2) {
                    r_idx--;
                }
                r_idx--;
            } else if (sum > 0) {
                while (nums[r_idx] == nums[r_idx - 1] && r_idx > i + 2) {
                    r_idx--;
                }
                r_idx--;
            } else {  // sum < 0
                while (nums[l_idx] == nums[l_idx + 1] && l_idx < len - 2) {
                    l_idx++;
                }
                l_idx++;
            }
        }
    }
}
```



## 16. 最接近的三数之和

![](D:\Notes\Leetcode\Leetcode.assets\16.png)

我的AC代码（C++）：

```c++
class Solution {
public:
	int len;
	int closestSum;
	int threeSumClosest(vector<int>& nums, int target) {
		sort(nums.begin(), nums.end());
		len = nums.size();
		closestSum = 0xfffffff;
		int i = 0;
		while (i < len - 2) {
			int l_idx = i + 1;
			int r_idx = len - 1;
			find(nums, i, l_idx, r_idx, target);
			if (closestSum == target) {
				break;
			}
			while (nums[i] == nums[i + 1] && i < len - 2) {
				i++;
			}
			i++;
		}
		return closestSum;
	}
	void find(vector<int>& nums, int i, int l_idx, int r_idx, int target) {
		while (l_idx < r_idx) {
			int sum = nums[i] + nums[l_idx] + nums[r_idx];
			if (abs(target - sum) < abs(target - closestSum)) {
				closestSum = sum;
			}
			if (sum == target) {
				return;
			}
			else if (sum > target) {
				while (nums[r_idx] == nums[r_idx - 1] && r_idx > i + 2) {
					r_idx--;
				}
				r_idx--;
			}
			else {  // sum < target
				while (nums[l_idx] == nums[l_idx + 1] && l_idx < len - 2) {
					l_idx++;
				}
				l_idx++;
			}
		}
	}
};
```

我的AC代码（Java）：

```java
class Solution {
    int len;
    int closestSum;

    public int threeSumClosest(int[] nums, int target) {
        Arrays.sort(nums);
        len = nums.length;
        closestSum = Integer.MAX_VALUE;
        int i = 0;
        while (i < len - 2) {
            int l_idx = i + 1;
            int r_idx = len - 1;
            find(nums, i, l_idx, r_idx, target);
            if (closestSum == target) {
                break;
            }
            while (nums[i] == nums[i + 1] && i < len - 2) {
                i++;
            }
            i++;
        }
        return closestSum;
    }

    void find(int[] nums, int i, int l_idx, int r_idx, int target) {
        while (l_idx < r_idx) {
            int sum = nums[i] + nums[l_idx] + nums[r_idx];
            if (Math.abs(target - sum) < Math.abs(target - closestSum)) {
                closestSum = sum;
            }
            if (sum == target) {
                return;
            } else if (sum > target) {
                while (nums[r_idx] == nums[r_idx - 1] && r_idx > i + 2) {
                    r_idx--;
                }
                r_idx--;
            } else {  // sum < target
                while (nums[l_idx] == nums[l_idx + 1] && l_idx < len - 2) {
                    l_idx++;
                }
                l_idx++;
            }
        }
    }
}
```



## 18. 四数之和

![](D:\Notes\Leetcode\Leetcode.assets\18.png)

相关视频：
[【忍者算法】LeetCode 18 四数之和](https://www.bilibili.com/video/BV1r341147JQ)

我的AC代码（C++）：

```c++
class Solution {
public:
	int len;
	vector<vector<int>> vv;
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
					j++;
				}
				j++;
			}
			while (nums[i] == nums[i + 1] && i < len - 3) {
				i++;
			}
			i++;
		}
		return vv;
	}
	void find(vector<int>& nums, int i, int j, int l_idx, int r_idx, int target) {
		while (l_idx < r_idx) {
			long long sum = (long long)nums[i] + (long long)nums[j] + (long long)nums[l_idx] + (long long)nums[r_idx];
			if (sum == (long long)target) {
				vector<int> v = { nums[i], nums[j], nums[l_idx], nums[r_idx] };
				vv.push_back(v);
				while (nums[l_idx] == nums[l_idx + 1] && l_idx < len - 2) {
					l_idx++;
				}
				l_idx++;
				while (nums[r_idx] == nums[r_idx - 1] && r_idx > j + 2) {
					r_idx--;
				}
				r_idx--;
			}
			else if (sum > (long long)target) {
				while (nums[r_idx] == nums[r_idx - 1] && r_idx > j + 2) {
					r_idx--;
				}
				r_idx--;
			}
			else {  // sum < (long long)target
				while (nums[l_idx] == nums[l_idx + 1] && l_idx < len - 2) {
					l_idx++;
				}
				l_idx++;
			}
		}
	}
};
```

我的AC代码（Java）：

```java
class Solution {
    int len;
    List<List<Integer>> ll;

    public List<List<Integer>> fourSum(int[] nums, int target) {
        Arrays.sort(nums);
        len = nums.length;
        ll = new ArrayList<>();
        int i = 0;
        while (i < len - 3) {
            int j = i + 1;
            while (j < len - 2) {
                int l_idx = j + 1;
                int r_idx = len - 1;
                find(nums, i, j, l_idx, r_idx, target);
                while (nums[j] == nums[j + 1] && j < len - 2) {
                    j++;
                }
                j++;
            }
            while (nums[i] == nums[i + 1] && i < len - 3) {
                i++;
            }
            i++;
        }
        return ll;
    }

    void find(int[] nums, int i, int j, int l_idx, int r_idx, int target) {
        while (l_idx < r_idx) {
            long sum = (long) nums[i] + (long) nums[j] + (long) nums[l_idx] + (long) nums[r_idx];
            if (sum == (long) target) {
                List<Integer> l = new ArrayList<>();
                l.add(nums[i]);
                l.add(nums[j]);
                l.add(nums[l_idx]);
                l.add(nums[r_idx]);
                ll.add(l);
                while (nums[l_idx] == nums[l_idx + 1] && l_idx < len - 2) {
                    l_idx++;
                }
                l_idx++;
                while (nums[r_idx] == nums[r_idx - 1] && r_idx > j + 2) {
                    r_idx--;
                }
                r_idx--;
            } else if (sum > (long) target) {
                while (nums[r_idx] == nums[r_idx - 1] && r_idx > j + 2) {
                    r_idx--;
                }
                r_idx--;
            } else {  // sum < (long) target
                while (nums[l_idx] == nums[l_idx + 1] && l_idx < len - 2) {
                    l_idx++;
                }
                l_idx++;
            }
        }
    }
}
```



## 26. 删除有序数组中的重复项

![](D:\Notes\Leetcode\Leetcode.assets\26.png)

我的AC代码（Java）：

```java
class Solution {
    public int removeDuplicates(int[] nums) {
        int cnt = 1;
        int len = nums.length;
        if (len < 2) {
            cnt = len;
            return cnt;
        }
        int l_idx = 0;
        int r_idx = 1;
        while (r_idx < len) {
            if (nums[l_idx] != nums[r_idx]) {
                l_idx++;
                nums[l_idx] = nums[r_idx];
                cnt++;
            }
            r_idx++;
        }
        return cnt;
    }
}
```



## 27. 移除元素

![](D:\Notes\Leetcode\Leetcode.assets\27.png)

我的AC代码（Java）：

```java
class Solution {
    public int removeElement(int[] nums, int val) {
        int cnt = 0;
        int len = nums.length;
        if (len == 0) {
            return cnt;
        } else if (len == 1) {
            return nums[0] == val ? cnt : ++cnt;
        }
        int l_idx = 0;
        int r_idx = 0;
        while (r_idx < len) {
            if (nums[r_idx] != val) {
                nums[l_idx] = nums[r_idx];
                l_idx++;
                cnt++;
            }
            r_idx++;
        }
        return cnt;
    }
}
```



## 167. 两数之和 II - 输入有序数组

![](D:\Notes\Leetcode\Leetcode.assets\167.png)

我的AC代码（Java）：

```java
class Solution {
    public int[] twoSum(int[] numbers, int target) {
        int len = numbers.length;
        int l_idx = 0;
        int r_idx = len - 1;
        int[] res = new int[2];
        while (l_idx < r_idx) {
            int sum = numbers[l_idx] + numbers[r_idx];
            if (sum == target) {
                res[0] = l_idx + 1;
                res[1] = r_idx + 1;
                break;
            } else if (sum > target) {
                while (numbers[r_idx] == numbers[r_idx - 1] && r_idx > 2) {
                    r_idx--;
                }
                r_idx--;
            } else {  // sum < target
                while (numbers[l_idx] == numbers[l_idx + 1] && l_idx < len - 2) {
                    l_idx++;
                }
                l_idx++;
            }
        }
        return res;
    }
}
```



## 345. 反转字符串中的元音字母

![](D:\Notes\Leetcode\Leetcode.assets\345.png)

我的AC代码（Java）：

```java
class Solution {
    public String reverseVowels(String s) {
        char[] c = s.toCharArray();
        int len = s.length();
        int l_idx = 0;
        int r_idx = len - 1;
        while (l_idx < r_idx) {
            char l_c = c[l_idx];
            char r_c = c[r_idx];
            boolean l_flag = isVowel(l_c);
            boolean r_flag = isVowel(r_c);
            if (l_flag && r_flag) {
                c[l_idx] = r_c;
                c[r_idx] = l_c;
                l_idx++;
                r_idx--;
            } else if (l_flag && !r_flag) {
                while (c[r_idx] == c[r_idx - 1] && r_idx > 2) {
                    r_idx--;
                }
                r_idx--;
            } else if (!l_flag && r_flag) {
                while (c[l_idx] == c[l_idx + 1] && l_idx < len - 2) {
                    l_idx++;
                }
                l_idx++;
            } else {  // !l_flag && !r_flag
                while (c[l_idx] == c[l_idx + 1] && l_idx < len - 2) {
                    l_idx++;
                }
                l_idx++;
                while (c[r_idx] == c[r_idx - 1] && r_idx > 2) {
                    r_idx--;
                }
                r_idx--;
            }
        }
        return new String(c);
    }

    boolean isVowel(char c) {
        switch (c) {
            case 'A':
            case 'E':
            case 'I':
            case 'O':
            case 'U':
            case 'a':
            case 'e':
            case 'i':
            case 'o':
            case 'u':
                return true;
            default:
        }
        return false;
    }
}
```



## 680. 验证回文串 II

![](D:\Notes\Leetcode\Leetcode.assets\680.png)

我的AC代码（Java）：

```java
class Solution {
    public boolean validPalindrome(String s) {
        int l_idx = 0;
        int r_idx = s.length() - 1;
        boolean flag = true;
        while (l_idx < r_idx) {
            char l_c = s.charAt(l_idx);
            char r_c = s.charAt(r_idx);
            if (l_c != r_c) {
                flag = false;
                break;
            }
            l_idx++;
            r_idx--;
        }
        return flag ? flag : isPalindrome(s, l_idx, r_idx - 1) || isPalindrome(s, l_idx + 1, r_idx);
    }

    boolean isPalindrome(String s, int l_idx, int r_idx) {
        if (l_idx > r_idx) {
            return false;
        }
        while (l_idx < r_idx) {
            char l_c = s.charAt(l_idx);
            char r_c = s.charAt(r_idx);
            if (l_c != r_c) {
                return false;
            }
            l_idx++;
            r_idx--;
        }
        return true;
    }
}
```



## 986. 区间列表的交集

![](D:\Notes\Leetcode\Leetcode.assets\986.png)

我的AC代码（Java）：

```java
class Solution {
    public int[][] intervalIntersection(int[][] firstList, int[][] secondList) {
        List<int[]> l = new ArrayList<>();
        int idx1 = 0;
        int idx2 = 0;
        while (idx1 < firstList.length && idx2 < secondList.length) {
            if (firstList[idx1][1] < secondList[idx2][0]) {
                idx1++;
                continue;
            }
            if (secondList[idx2][1] < firstList[idx1][0]) {
                idx2++;
                continue;
            }
            // firstList[idx1][1] >= secondList[idx2][0]
            // secondList[idx2][1] >= firstList[idx1][0]
            int start = Math.max(firstList[idx1][0], secondList[idx2][0]);
            int end = Math.min(firstList[idx1][1], secondList[idx2][1]);
            int[] interval = {start, end};
            l.add(interval);
            if (firstList[idx1][1] == end) {
                idx1++;
            }
            if (secondList[idx2][1] == end) {
                idx2++;
            }
        }
        int[][] res = new int[l.size()][];
        int i = 0;
        for (int[] interval : l) {
            res[i] = interval;
            i++;
        }
        return res;
    }
}
```

