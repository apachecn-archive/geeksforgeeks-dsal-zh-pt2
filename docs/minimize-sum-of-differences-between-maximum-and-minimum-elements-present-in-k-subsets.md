# 最小化 K 个子集存在的最大和最小元素之差的总和

> 原文:[https://www . geeksforgeeks . org/minimum-最大和最小元素之间的差异之和-存在于 k 个子集中/](https://www.geeksforgeeks.org/minimize-sum-of-differences-between-maximum-and-minimum-elements-present-in-k-subsets/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**和一个整数 **K** ，任务是通过将数组拆分为 **K** [个子集](https://www.geeksforgeeks.org/backtracking-to-find-all-subsets/)来最小化每个子集的最大元素和最小元素之间的差之和，使得每个子集仅由唯一的数组元素组成。

**示例:**

> **输入:** arr[] = { 6，3，8，1，3，1，2，2 }，K = 4
> **输出:** 6
> **解释:**
> 将数组拆分为 K(= 4)个子集的最佳方式之一是{ { 1，2 }、{ 2，3 }、{ 6，8 }、{ 1，4 } }。
> 每个子集存在的最大和最小元素之差的和= {(2–1)+(3–2)+(8–6)+(3–1)} = 6。
> 因此，要求的输出为 6
> 
> **输入:** arr[] = { 2，2，1，1 }，K = 1
> **输出:** -1

**方法:**使用[带位屏蔽的动态规划](https://www.geeksforgeeks.org/bitmasking-and-dynamic-programming-set-1-count-ways-to-assign-unique-cap-to-every-person/)可以解决问题。以下是循环关系:

> **掩码:** i <sup>第</sup>位掩码检查数组元素是否已经在子集内被选中。
> **l:** 子集中选定的最后一个元素的索引。
> **j:** 子集中选中的当前元素的索引。
> 
> 如果掩码 mod(n/k)= = 1:
> DP[掩码][l]= min(DP[掩码][l]，DP[掩码^ (1 < < l)][j])
> 
> 否则，<DP[mask][j]= min(DP[mask][j]，DP[mask ^(1<<j)][l]+num[l]-num[j])

按照以下步骤解决问题:

*   迭代**掩码**的所有可能值，即**【0，2<sup>N</sup>–1】**
*   初始化一个数组，比如 **n_z_bits[]** ，以存储已经在子集中选择的元素的计数。
*   使用上述递归关系并填充递归关系的所有可能的 dp 状态。
*   最后，打印从 **dp[(1 < < N ) - 1]** 开始的最小元素。

下面是上述方法的实现:

## 蟒蛇 3

```
# Python program to implement
# the above approach
from itertools import permutations 
from itertools import combinations

# Function to minimize the sum of
# difference between maximums and
# minimums of K subsets of an array
def MinimizeSum(nums, k):

    # Stores count of elements
    # in an array
    n = len(nums)

    # Base Case
    if k == n:
        return 0

    # Initialize DP[][] array
    dp = [[float("inf")] * n for _ in range(1 << n)]

    # Sort the array
    nums.sort()

    # Mark i-th element
    # as not selected
    for i in range(n):
        dp[1 << i][i] = 0

    # Iterate over all possible
    # values of mask
    for mask in range(1 << n):

        # Store count of set bits
        # in mask
        n_z_bits = []

        # Store index of element which is 
        # already selected in a subset
        for p, c in enumerate(bin(mask)): 
            if c == "1":
                temp = len(bin(mask)) - p - 1
                n_z_bits.append(temp)

        # If count of set bits in mask
                # mod (n // k) equal to 1
        if len(n_z_bits) % (n//k) == 1:
            for j, l in permutations(n_z_bits, 2):
                temp = dp[mask ^ (1 << l)][j]
                dp[mask][l] = min(dp[mask][l], temp)

        else:
            for j, l in combinations(n_z_bits, 2):
                if nums[j] != nums[l]:

                    # Check if l-th element 
                    # is already selected or not
                    mask_t = mask ^ (1 << l)

                    temp = (dp[mask_t][j] + 
                             nums[j] - nums[l])

                    # Update dp[mask][l]        
                    dp[mask][l] = min(dp[mask][l],
                                            temp)

    # Return minimum element 
    # from dp[(1 << N) - 1]
    if min(dp[-1]) != float("inf"):
        return min(dp[-1])

    # If dp[-1] is inf then the 
    # partition is not possible 
    else: 
        return -1

# Driver Code
if __name__ == "__main__":
    # Given array
    arr = [ 6, 3, 8, 1, 3, 1, 2, 2 ]
    K = 4

    # Function call
    print(MinimizeSum(arr, K))
```

**Output:**

```
6

```

***时间复杂度:**O(N * 2<sup>N</sup>)*
***辅助空间:*** O(N * 2 <sup>N</sup>