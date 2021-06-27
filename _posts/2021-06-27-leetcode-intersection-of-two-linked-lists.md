---
layout:     post

title:      LeetCode

subtitle:   intersection-of-two-linked-lists

date:       2021-06-27

author:     月光下的海

header-img: img/4.jpg
catalog: true

tags:

    - leetcode

---


#### 题目描述
给你两个单链表的头节点 headA 和 headB ，请你找出并返回两个单链表相交的起始节点。如果两个链表没有交点，返回 null 。

题目数据 保证 整个链式结构中不存在环。

注意，函数返回结果后，链表必须 保持其原始结构。

- 示例 1：

输入：intersectVal = 8, listA = [4,1,8,4,5], listB = [5,0,1,8,4,5], skipA = 2, skipB = 3
输出：Intersected at '8'


######  进阶：你能否设计一个时间复杂度 O(n) 、仅用 O(1) 内存的解决方案？


来源：力扣（LeetCode）
链接：[https://leetcode-cn.com/problems/intersection-of-two-linked-lists](https://leetcode-cn.com/problems/intersection-of-two-linked-lists)
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```java

package com.anthony.algorithm;

import java.util.HashSet;
import java.util.Set;

/**
 * 给你两个单链表的头节点 headA 和 headB ，请你找出并返回两个单链表相交的起始节点。如果两个链表没有交点，返回 null 。
 * Created by luxb on 2021/6/27
 */
public class GetIntersectionNode {
    //借助Set,容易看懂但比较低效
    public static ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        if(headA == null || headB == null){
            return null;
        }
        Set<ListNode> set = new HashSet<>();
        ListNode node = headA;
        while (node != null) {
            set.add(node);
            node = node.next;
        }
        node = headB;
        while (node != null) {
            if (set.contains(node)) {
                return node;
            }
            node = node.next;
        }
        return null;
    }

    public static void main(String[] args) {
        ListNode headA = new ListNode(8);
        ListNode headB = new ListNode(4);
        headB.next = new ListNode(1);
        headB.next.next = new ListNode(8);
        headB.next.next.next = new ListNode(4);
        headB.next.next.next.next = new ListNode(5);
        System.out.println(getIntersectionNode(headA, headB));
    }
}



```