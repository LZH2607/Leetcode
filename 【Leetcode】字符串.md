# 【Leetcode】字符串



[toc]



## 58. 最后一个单词的长度

![](D:\Notes\Leetcode\Leetcode.assets\58-1.png)
![](D:\Notes\Leetcode\Leetcode.assets\58-2.png)

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

![](D:\Notes\Leetcode\Leetcode.assets\125-1.png)
![](D:\Notes\Leetcode\Leetcode.assets\125-2.png)

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

![](D:\Notes\Leetcode\Leetcode.assets\151-1.png)
![](D:\Notes\Leetcode\Leetcode.assets\151-2.png)

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

