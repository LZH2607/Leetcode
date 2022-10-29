# 【Leetcode】字符串



[toc]



## 58. 最后一个单词的长度

![](D:\Notes\Leetcode\Leetcode.assets\58.png)

我的AC代码（Java）：

```java
class Solution {
    public int lengthOfLastWord(String s) {
        ArrayList<String> strList = new ArrayList<>(Arrays.asList(s.split("\\s+")));
        strList.remove("");
        return strList.get(strList.size() - 1).length();
    }
}
```



## 125. 验证回文串

![](D:\Notes\Leetcode\Leetcode.assets\125.png)

我的AC代码（Java）：

```java
class Solution {
    public boolean isPalindrome(String s) {
        s = s.replaceAll("[^A-Za-z0-9]", "").toLowerCase();
        for (int i = 0; i < s.length() / 2; i++) {
            if (s.charAt(i) != s.charAt(s.length() - 1 - i)) {
                return false;
            }
        }
        return true;
    }
}
```



## 151. 反转字符串中的单词

![](D:\Notes\Leetcode\Leetcode.assets\151.png)

我的AC代码（Java）：

```java
class Solution {
    public String reverseWords(String s) {

        ArrayList<String> strList = new ArrayList<>(Arrays.asList(s.split("\\s+")));
        strList.remove("");
        String res = strList.get(strList.size() - 1);
        for (int i = strList.size() - 2; i >= 0; i--) {
            res += " " + strList.get(i);
        }
        return res;
    }
}
```



## 434. 字符串中的单词数

![](D:\Notes\Leetcode\Leetcode.assets\434.png)

我的AC代码（Java）：

```java
class Solution {
    public int countSegments(String s) {
        ArrayList<String> strList = new ArrayList<>(Arrays.asList(s.split("\\s+")));
        strList.remove("");
        return strList.size();
    }
}
```



## 1790. 仅执行一次字符串交换能否使两个字符串相等

![](D:\Notes\Leetcode\Leetcode.assets\1790.png)

我的AC代码（Java）：

```java
class Solution {
    public boolean areAlmostEqual(String s1, String s2) {
        if (s1.equals(s2)) {
            return true;
        }
        int idx1 = -1;
        int idx2 = -1;
        for (int i = 0; i < s1.length(); i++) {
            if (s1.charAt(i) == s2.charAt(i)) {
                continue;
            }
            // s1.charAt(i) != s2.charAt(i)
            if (idx1 < 0) {
                idx1 = i;
                continue;
            }
            if (idx2 < 0) {
                idx2 = i;
                continue;
            }
            return false;
        }
        return idx2 >= 0 && (s1.charAt(idx1) == s2.charAt(idx2) && s1.charAt(idx2) == s2.charAt(idx1));
    }
}
```



## 2414. 最长的字母序连续子字符串的长度

![](D:\Notes\Leetcode\Leetcode.assets\2414.png)

我的AC代码（Java）：

```java
class Solution {
    public int longestContinuousSubstring(String s) {
        char[] arr = s.toCharArray();
        int len = 1;
        int max_len = 1;
        for (int i = 1; i < arr.length; i++) {
            if (arr[i] - arr[i - 1] == 1) {
                len++;
            } else {
                len = 1;
            }
            if (max_len < len) {
                max_len = len;
            }
        }
        return max_len;
    }
}
```

