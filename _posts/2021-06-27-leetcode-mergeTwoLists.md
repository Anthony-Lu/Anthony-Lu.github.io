---
layout:     post

title:      LeetCode

subtitle:   mergeTwoLists

date:       2021-06-27

author:     月光下的海

header-img: img/post-bg-2015.jpg
catalog: true

tags:

    - leetcode

---


#### 题目描述
将两个升序链表合并为一个新的 升序 链表并返回。新链表是通过拼接给定的两个链表的所有节点组成的。

- 示例 1：

输入：l1 = [1,2,4], l2 = [1,3,4]
输出：[1,1,2,3,4,4]
- 示例 2：

输入：l1 = [], l2 = []
输出：[]
- 示例 3：

输入：l1 = [], l2 = [0]
输出：[0]

######  提示：
- 两个链表的节点数目范围是 [0, 50]
- 100 <= Node.val <= 100
- l1 和 l2 均按 非递减顺序 排列

来源：力扣（LeetCode）
链接：[https://leetcode-cn.com/problems/merge-two-sorted-lists/](https://leetcode-cn.com/problems/merge-two-sorted-lists/)
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```java

package com.anthony.algorithm;
public class mergeTwoLists {
    public static class ListNode {
        int val;
        ListNode next = null;
        public ListNode(int val) {
            this.val = val;
        }
        @Override
        public String toString() {
            StringBuilder sb = new StringBuilder();
            ListNode head = this;
            while (head != null){
                sb.append(head.val + "  ");
                head = head.next;
            }
            return sb.toString();
        }
    }

    public ListNode mergeTwoLists (ListNode l1, ListNode l2) {
        if(l1 == null){
            return l2;
        }
        if(l2 == null){
            return l1;
        }
        ListNode dummy = new ListNode(0);
        ListNode head = dummy;
        while (l1 != null && l2 != null){
            if(l1.val < l2.val){
                head.next = l1;
                l1 = l1.next;
            }else{
                head.next = l2;
                l2 = l2.next;
            }
            head = head.next;
        }
        head.next = l1 == null ? l2 : l1;
        return dummy.next;
    }

    public static void main(String[] args) {
        ListNode l1 = new ListNode(1);
        l1.next = new ListNode(2);
        l1.next.next = new ListNode(3);
        ListNode l2 = new ListNode(1);
        l2.next = new ListNode(2);
        l2.next.next = new ListNode(4);
        ListNode listNode = new mergeTwoLists().mergeTwoLists(l1, l2);
        System.out.println(listNode.toString());
    }
}


```