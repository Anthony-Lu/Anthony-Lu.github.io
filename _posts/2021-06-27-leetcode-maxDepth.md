---
layout:     post

title:      LeetCode

subtitle:   maxDepth

date:       2021-06-27

author:     月光下的海

header-img: img/10.jpg

catalog: true

tags:

    - leetcode

---

#### 题目描述

给定一个二叉树，找出其最大深度。

二叉树的深度为根节点到最远叶子节点的最长路径上的节点数。

- 示例：

    -   输入: 给定二叉树 [3,9,20,null,null,15,7]，
    -   输出：返回它的最大深度 3 。

来源：力扣（LeetCode）
链接：[https://leetcode-cn.com/problems/maximum-depth-of-binary-tree/](https://leetcode-cn.com/problems/maximum-depth-of-binary-tree/)
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

```java

/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public int maxDepth(TreeNode root) {
        if (root == null) {
            return 0;
        }
        return Math.max(maxDepth(root.left), maxDepth(root.right)) + 1;
    }
}


```