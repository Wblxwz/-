#### [88. 合并两个有序数组 - 力扣（LeetCode）](https://leetcode.cn/problems/merge-sorted-array/description/?envType=study-plan-v2&envId=top-interview-150)

给你两个按 **非递减顺序** 排列的整数数组 `nums1` 和 `nums2`，另有两个整数 `m` 和 `n` ，分别表示 `nums1` 和 `nums2` 中的元素数目。

请你 **合并** `nums2` 到 `nums1` 中，使合并后的数组同样按 **非递减顺序** 排列。

**注意：**最终，合并后数组不应由函数返回，而是存储在数组 `nums1` 中。为了应对这种情况，`nums1` 的初始长度为 `m + n`，其中前 `m` 个元素表示应合并的元素，后 `n` 个元素为 `0` ，应忽略。`nums2` 的长度为 `n` 。

##### 解法1：双指针

新建一个sorted数组，排序给sorted，然后赋值回去给nums1	

时间复杂度O(m+n)

空间复杂度O(m+n)

##### 解法2：逆向双指针

nums1的后半部分是空的，可以直接覆盖而不会影响结果。因此可以指针设置为从后向前遍历，每次取两者之中的较大者放进 nums1的最后面。*p*1 后面的位置永远足够容纳被插入的元素，不会产生 p1的元素被覆盖的情况。证明详见题解

时间复杂度O(m+n)

空间复杂度O(1)

#### [27. 移除元素 - 力扣（LeetCode）](https://leetcode.cn/problems/remove-element/description/?envType=study-plan-v2&envId=top-interview-150)

给你一个数组 `nums` 和一个值 `val`，你需要 **[原地](https://baike.baidu.com/item/原地算法)** 移除所有数值等于 `val` 的元素，并返回移除后数组的新长度。

不要使用额外的数组空间，你必须仅使用 `O(1)` 额外空间并 **[原地 ](https://baike.baidu.com/item/原地算法)修改输入数组**。

元素的顺序可以改变。你不需要考虑数组中超出新长度后面的元素。

##### 解法1：双指针

检索所有值，如果等于val就将右指针右移，否则说明可以保留该元素，就将右指针的值赋给左指针，然后都右移

时间复杂度 O(n)

空间复杂度 O(1)