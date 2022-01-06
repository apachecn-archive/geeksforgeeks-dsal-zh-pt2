# 具有二进制等价的给定数组的子序列计数

> 原文:[https://www . geeksforgeeks . org/给定数组的子序列计数具有二进制等价性/](https://www.geeksforgeeks.org/count-of-subsequences-from-a-given-array-having-binary-equivalence/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是找到具有**二元等价**的不同子序列的总数[。](https://www.geeksforgeeks.org/count-distinct-subsequences/)

> 如果子序列中所有十进制数的二进制表示中的**设置**和**未设置**位的计数之和相等，则子序列具有**二进制等价**。

**示例:**

> ***输入:*** *arr[] = {2，7，10}*
> ***输出:**0011*
> T12】解释:
> 2 → 0010→1 的 s = 1，0 的 s = 3
> 7 → 0111→1 的 s = 3，0 的 s = 1
> 10 → 1010→1 的 s = 2，0 的 s = 1
> 同样，【2，7】也各有 4 的二进制等价。
> 但[7，10]不具有二元等价性。
> 同样，【10】的二进制等价为 2。
> 二进制等价的唯一子序列的总数是 3。
> 由于 10 是给定数组中最大的元素，用二进制表示 10 所需的位数是 4。因此，输出中的位数需要为 4。
> 
> ***输入:*** arr[] = { *5、7、9、12}*
> ***输出:** 0111*

**方法:**想法是找到表示数组的[最大元素所需的总位数。请按照以下步骤解决此问题:](https://www.geeksforgeeks.org/c-program-find-largest-element-array/)

1.  求最大元素和最大元素的二进制表示长度。
2.  在[二进制表示](https://www.geeksforgeeks.org/binary-representation-of-a-given-number/)的其他元素前面追加 **0** ，使每个元素的位数等于最大位数。
3.  [找到给定数组的所有子序列](https://www.geeksforgeeks.org/generating-all-possible-subsequences-using-recursion/)。
4.  求**二进制等价**的子序列总数。
5.  将总数转换为二进制数，如果总数的长度小于最大数的长度，则追加 **0s** ，使两个长度相等。

下面是上述方法的实现:

## 蟒蛇 3

```
# Python program for the above approach
import itertools

# Function to find the number of
# subsequences having Binary Equivalence
def numberOfSubsequence(arr):

    # Find the maximum array element
    Max_element = max(arr)

    # Convert the maximum element
    # to its binary equivalent
    Max_Binary = "{0:b}".format(int(
        Max_element))

    # Dictionary to store the count of
    # set and unset bits of all array elements
    Dic = {}

    for i in arr:
        Str = "{0:b}".format(int(i))

        if len(Str) <= len(Max_Binary):
            diff = len(Max_Binary)-len(Str)

            # Add the extra zeros before all
            # the elements which have length
            # smaller than the maximum element
            Str = ('0'*diff)+Str

        zeros = Str.count('0')
        ones = Str.count('1')

        # Fill the dictionary with number
        # of 0's and 1's
        Dic[int(i)] = [zeros, ones]

    all_combinations = []

    # Find all the combination
    for r in range(len(arr)+1):

        comb = itertools.combinations(arr, r)
        comlist = list(comb)
        all_combinations += comlist
    count = 0

    # Find all the combinations where
    # sum_of_zeros == sum_of_ones
    for i in all_combinations[1:]:
        sum0 = 0
        sum1 = 0
        for j in i:
            sum0 += Dic[j][0]
            sum1 += Dic[j][1]

        # Count the total combinations
        # where sum_of_zeros = sum_of_ones
        if sum0 == sum1:
            count += 1

    # Convert the count number to its
    # binary equivalent
    Str = "{0:b}".format(int(count))
    if len(Str) <= len(Max_Binary):
        diff = len(Max_Binary)-len(Str)

        # Append leading zeroes to
        # the answer if its length is
        # smaller than the maximum element
        Str = ('0'*diff) + Str

    # Print the result
    print(Str)

# Driver Code

# Give array arr[]
arr = [5, 7, 9, 12]

# Function Call
numberOfSubsequence(arr)
```

**Output:** 

```
0111
```

***时间复杂度:**O(2<sup>N</sup>)*
***辅助空间:** O(N <sup>2</sup> )*