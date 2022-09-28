# 【Leetcode】单链表



[toc]



单链表结点的定义（Java）：

```java
public class ListNode {
    int val;
    ListNode next;
    ListNode() {}
    ListNode(int val) { this.val = val; }
    ListNode(int val, ListNode next) { this.val = val; this.next = next; }
}
```



## 2. 两数相加

![](D:\Notes\Leetcode\Leetcode.assets\2-1.png)
![](D:\Notes\Leetcode\Leetcode.assets\2-2.png)

我的AC代码（Java）：

```java
class Solution {
    public static ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode l3 = new ListNode();
        ListNode p = l3;
        int s;
        int d;
        int c = 0;
        while (l1 != null && l2 != null) {
            s = l1.val + l2.val + c;
            d = s % 10;
            c = s / 10;
            p.next = new ListNode(d);
            p = p.next;
            l1 = l1.next;
            l2 = l2.next;
        }
        if (l1 == null && l2 != null) {
            while (l2 != null) {
                s = l2.val + c;
                d = s % 10;
                c = s / 10;
                p.next = new ListNode(d);
                p = p.next;
                l2 = l2.next;
            }
        } else if (l1 != null && l2 == null) {
            while (l1 != null) {
                s = l1.val + c;
                d = s % 10;
                c = s / 10;
                p.next = new ListNode(d);
                p = p.next;
                l1 = l1.next;
            }
        }
        if (c != 0) {
            p.next = new ListNode(c);
        }
        return l3.next;
    }
}
```



## 19. 删除链表的倒数第 N 个结点

![](D:\Notes\Leetcode\Leetcode.assets\19-1.png)
![](D:\Notes\Leetcode\Leetcode.assets\19-2.png)

我的AC代码（Java，解法1，两趟遍历）：

```java
class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {
        ListNode p = head;
        int len = 0;
        while (p != null) {
            len++;
            p = p.next;
        }
        if (len == 1 || len == n) {
            head = head.next;
        } else {  // 删除倒数第n个结点 = 删除正数第len-n+1个结点（从1开始计数）
            p = head;
            for (int i = 1; i < len - n; i++) {
                p = p.next;
            }
            p.next = p.next.next;
        }
        return head;
    }
}
```

我的AC代码（Java，解法2，一趟遍历）：

```java
class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {
        List<ListNode> l = new ArrayList<>();
        ListNode p = head;
        int len = 0;
        while (p != null) {
            l.add(p);
            len++;
            p = p.next;
        }
        if (len == 1 || len == n) {
            head = head.next;
        } else {  // 删除倒数第n个结点 = 删除正数第len-n+1个结点（从1开始计数）
            l.get(len - n - 1).next = l.get(len - n - 1).next.next;
        }
        return head;
    }
}
```

