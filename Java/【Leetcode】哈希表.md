# 【Leetcode】哈希表



[toc]



## 1. 两数之和

![](D:\Notes\Leetcode\Leetcode.assets\1-1.png)
![](D:\Notes\Leetcode\Leetcode.assets\1-2.png)

相关视频：
[二数之和题解分析](https://www.bilibili.com/video/BV1hV411e7MW)
[二数之和代码解析](https://www.bilibili.com/video/BV1si4y1P7Eg)

我的AC代码：

```java
class Solution {
	public int[] twoSum(int[] nums, int target) {
		HashMap<Integer, Integer> m = new HashMap<>();
		int len = nums.length;
		int ans[] = new int[2];
		for (int i = 0; i < len; i++) {
			if (m.containsKey(target - nums[i])) {
				ans[0] = i;
				ans[1] = m.get(target - nums[i]);
				break;
			} else {
				m.put(nums[i], i);
			}
		}
		return ans;
	}
}
```



## 12. 整数转罗马数字

![](D:\Notes\Leetcode\Leetcode.assets\12-1.png)
![](D:\Notes\Leetcode\Leetcode.assets\12-2.png)
![](D:\Notes\Leetcode\Leetcode.assets\12-3.png)

相关视频：
[你真的识数么？一起认识罗马数字](https://www.bilibili.com/video/BV19541157Pm)
[罗马数字Roman Numerals](https://www.bilibili.com/video/BV1fx411b7HX)
[五分钟力扣 Leetcode 第12题 整数转罗马数字  Python入门算法刷题 两种解法 Leetcode删除了什么功能大揭秘](https://www.bilibili.com/video/BV1ft4y1m7SK)

我的AC代码：

```java
class Solution {
	public String intToRoman(int num) {
		HashMap<Integer, String> m = new HashMap<>();
		m.put(0, "");
		m.put(1, "I");
		m.put(2, "II");
		m.put(3, "III");
		m.put(4, "IV");
		m.put(5, "V");
		m.put(6, "VI");
		m.put(7, "VII");
		m.put(8, "VIII");
		m.put(9, "IX");

		m.put(10, "X");
		m.put(20, "XX");
		m.put(30, "XXX");
		m.put(40, "XL");
		m.put(50, "L");
		m.put(60, "LX");
		m.put(70, "LXX");
		m.put(80, "LXXX");
		m.put(90, "XC");

		m.put(100, "C");
		m.put(200, "CC");
		m.put(300, "CCC");
		m.put(400, "CD");
		m.put(500, "D");
		m.put(600, "DC");
		m.put(700, "DCC");
		m.put(800, "DCCC");
		m.put(900, "CM");

		m.put(1000, "M");
		m.put(2000, "MM");
		m.put(3000, "MMM");

		String s = "";
		int base = 1;
		while (num > 0) {
			int res = num % 10;
			num = num / 10;
			s = m.get(res * base) + s;
			base *= 10;
		}

		return s;
	}
}
```



## 13. 罗马数字转整数

![](D:\Notes\Leetcode\Leetcode.assets\13-1.png)
![](D:\Notes\Leetcode\Leetcode.assets\13-2.png)
![](D:\Notes\Leetcode\Leetcode.assets\13-3.png)

我的AC代码：

```java
class Solution {
	public int romanToInt(String s) {
		HashMap<String, Integer> m = new HashMap<>();
		m.put("I", 1);
		m.put("II", 2);
		m.put("III", 3);
		m.put("IV", 4);
		m.put("V", 5);
		m.put("VI", 6);
		m.put("VII", 7);
		m.put("VIII", 8);
		m.put("IX", 9);

		m.put("X", 10);
		m.put("XX", 20);
		m.put("XXX", 30);
		m.put("XL", 40);
		m.put("L", 50);
		m.put("LX", 60);
		m.put("LXX", 70);
		m.put("LXXX", 80);
		m.put("XC", 90);

		m.put("C", 100);
		m.put("CC", 200);
		m.put("CCC", 300);
		m.put("CD", 400);
		m.put("D", 500);
		m.put("DC", 600);
		m.put("DCC", 700);
		m.put("DCCC", 800);
		m.put("CM", 900);

		m.put("M", 1000);
		m.put("MM", 2000);
		m.put("MMM", 3000);

		int num = 0;
		while (s.length() > 0) {
			int len = s.length();
			for (int l = 4; l > 0; l--) {
				if (len < l) {
					continue;
				}
				String subs = s.substring(0, l);
				if (m.containsKey(subs)) {
					num += m.get(subs);
					s = s.substring(l);
					break;
				}
			}
		}
		return num;
	}
}
```



## 49. 字母异位词分组

![](D:\Notes\Leetcode\Leetcode.assets\49-1.png)
![](D:\Notes\Leetcode\Leetcode.assets\49-2.png)

我的AC代码：

```java
class Solution {
	public List<List<String>> groupAnagrams(String[] strs) {
		HashMap<String, List<String>> m = new HashMap<>();
		for (int i = 0; i < strs.length; i++) {
			char cs[] = strs[i].toCharArray();
			Arrays.sort(cs);
			String k = new String(cs);
			if (m.containsKey(k)) {
				m.get(k).add(strs[i]);
			} else {
				List<String> l = new ArrayList<>();
				l.add(strs[i]);
				m.put(k, l);
			}
		}
		List<List<String>> ll = new ArrayList<>();
		for (List<String> l : m.values()) {
			ll.add(l);
		}
		return ll;
	}
}
```



## 128. 最长连续序列

![](D:\Notes\Leetcode\Leetcode.assets\128.png)

相关视频：
[最长连续序列](https://www.bilibili.com/video/BV1M7411A79B)

我的AC代码：

```java

```

