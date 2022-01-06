# 两个给定数组的子序列中可能的最大 K 位数

> 原文:[https://www . geeksforgeeks . org/两个给定数组的最大可能 k 位数/](https://www.geeksforgeeks.org/maximum-k-digit-number-possible-from-subsequences-of-two-given-arrays/)

给定两个 [数组](https://www.geeksforgeeks.org/array-data-structure/)**arr 1【】**和**arr 2【】**长度为 **M** 和 **N** 的数组，由代表两个数字的数字**【0，9】**和一个整数 **K** ( **K ≤ M + N** )组成，任务是通过

**例:**

> **输入:** arr1[] = {3，4，6，5}，arr2[] = {9，1，2，5，8，3}，K = 5
> **输出:** 98653
> **解释:**长度为 K 的给定数组 arr1[]和 arr2[]可以组成的最大个数为 98653。
> 
> **输入:** arr1[] = {6，7}，arr2[] = {6，0，4}，K = 5
> **输出:** 67604
> **解释:**长度为 K 的给定数组 arr1[]和 arr2[]可以形成的最大个数为 67604。

**天真方法:**想法是在**【0，K】**范围内 **s1** 的所有值上，从**arr 1【】**生成长度为 **s1** 的所有子序列，从数组**arr 2【】**生成长度为**(K–S1)**的所有子序列，并跟踪每次迭代中通过合并两个数组而形成的最大数。

***时间复杂度:**O(2<sup>N</sup>)*
***辅助空间:** O(1)*

**高效方法:**对上述方法进行优化，思路是从数组 **arr1[]** 和长度 **s1** 中获取最大数量，从数组 **arr2[]** 和长度**(K–S1)**中获取最大数量。然后，合并两个数组，得到最大长度数 **K** 。按照以下步骤解决给定的问题:

1.  使用变量 **i** 迭代范围**【0，K】**，并生成长度为 **i** 的所有可能的递减子序列，保持与数组**arr 1【】**相同的顺序，以及长度为**(K–I)**的子序列，遵循与数组**arr 2【】**相同的顺序。
2.  要在上述步骤中生成任意数组**arr【】**的长度 **L** 的递减子序列，请执行以下操作:
    *   初始化一个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**ans【】**来存储长度为 **L** 的子序列，保持与**arr【】**和[相同的顺序，遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)**arr【】**并执行以下操作:
        *   直到最后一个元素小于当前元素，然后从数组**和**中移除最后一个元素。
        *   如果 **ans[]** 的长度小于 **L** ，则在 **ans[]** 中插入当前元素。
    *   在上述步骤之后，结果子序列中的数组**和**。
3.  在**步骤 1** 中使用**步骤 2** 中讨论的方法生成所有可能长度的子序列时，通过合并所形成的两个子序列来生成最大数。
4.  完成上述步骤后，打印合并后给出最大数目的子序列。

下面是上述方法的实现:

## 蟒蛇 3

```
# Python program for the above approach

# Function to find maximum K-digit number
# possible from subsequences of the
# two arrays nums1[] and nums2[]
def maxNumber(nums1, nums2, k):

    # Store lengths of the arrays
    l1, l2 = len(nums1), len(nums2)

    # Store the resultant subsequence
    rs = []

    # Function to calculate maximum 
    # number from nums of length c_len
    def helper(nums, c_len):

        # Store the resultant maximum
        ans = []  

        # Length of the nums array
        ln = len(nums)

        # Traverse the nums array
        for idx, val in enumerate(nums):
            while ans and ans[-1] < val and ln-idx > c_len-len(ans):

                # If true, then pop
                # out the last element
                ans.pop(-1)  

            # Check the length with
            # required length
            if len(ans) < c_len: 

                # Append the value to ans
                ans.append(val)

        # Return the ans
        return ans  

    # Traverse and pick the maximum
    for s1 in range(max(0, k-l2), min(k, l1)+1):

        # p1 and p2 stores maximum number possible
        # of length s1 and k - s1 from
        # the arrays nums1[] & nums2[]
        p1, p2 = helper(nums1, s1), helper(nums2, k-s1)

        # Update the maximum number
        rs = max(rs, [max(p1, p2).pop(0) for _ in range(k)])

    # Return the result
    return rs  

# Driver Code

arr1 = [3, 4, 6, 5]
arr2 = [9, 1, 2, 5, 8, 3]

K = 5

# Function Call
print(maxNumber(arr1, arr2, K))
```

**Output:**

```
[9, 8, 6, 5, 3]

```

***时间复杂度:** O(K*(M + N))*
***辅助空间:** O(K)*