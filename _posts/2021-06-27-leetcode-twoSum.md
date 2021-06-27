---
layout:     post

title:      LeetCode

subtitle:   twoSum

date:       2021-06-27

author:     月光下的海

header-img: img/30.jpg

catalog: true

tags:

    - leetcode

---


#### 题目描述
给定一个整数数组 nums 和一个整数目标值 target，请你在该数组中找出 和为目标值 target  的那 两个 整数，并返回它们的数组下标。

你可以假设每种输入只会对应一个答案。但是，数组中同一个元素在答案里不能重复出现。

你可以按任意顺序返回答案。

- 示例 1：

输入：nums = [2,7,11,15], target = 9
输出：[0,1]
解释：因为 nums[0] + nums[1] == 9 ，返回 [0, 1] 。

- 示例 2：
  
  输入：nums = [3,2,4], target = 6
  输出：[1,2]
  
- 示例 3：

输入：nums = [3,3], target = 6
输出：[0,1]


######  提示：
- 2 <= nums.length <= 104
- -109 <= nums[i] <= 109
- -109 <= target <= 109
- 只会存在一个有效答案

###### 进阶
- 你可以想出一个时间复杂度小于 O(n2) 的算法吗？

来源：力扣（LeetCode）
链接：[https://leetcode-cn.com/problems/two-sum/](https://leetcode-cn.com/problems/two-sum/)
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
```java

package com.anthony.algorithm;
/**
 * Created by luxb on 2021/06/24 下午7:54
 */
public class TwoSum {
    //双重循环暴力破解
    public static int[] twoSum(int[] a, int target) {
        for (int i = 0; i < a.length; i++) {
            for (int j = i + 1; j < a.length; j++) {
                if (a[i] + a[j] == target) {
                    return new int[]{i, j};
                }
            }
        }
        return new int[0];
    }

    public static int[] newTwoSum(int[] a, int target) {
        //借助哈希表
        Map<Integer, Integer> map = new HashMap<>();
        int[] result = new int[2];
        for (int i = 0; i < a.length; i++) {
            if (map.containsKey(target - a[i])) {
                result[0] = map.get(target - a[i]);
                result[1] = i;
                return result;
            }
            map.put(a[i], i);
        }
        return result;
    }
}


```