# 通过替换缺失处的字符使字符串在每 K 个字符后重复

> 原文:[https://www . geesforgeks . org/make-string-repeating-after-k-characters-by-replace-in-missing-place/](https://www.geeksforgeeks.org/make-string-repeating-after-every-k-characters-by-replacing-characters-at-missing-place/)

给定一个[字符串](https://www.geeksforgeeks.org/category/data-structures/c-strings/) **S** 和整数 **K** 和还有一些缺失的字符即 **( _)，**任务是通过在缺失的地方即 **( _)替换合适的字符，使[字符串](https://www.geeksforgeeks.org/category/data-structures/c-strings/) **S** 在每一个 **K** 字符之后重复。**如果不可能，则打印 **-1。**

> **注意:**如果有多个可能的字符串，则打印[最小的字典序字符串。](https://www.geeksforgeeks.org/lexicographically-smallest-string-obtained-concatenating-array/)

**示例:**

> **输入:** S = ab_bab，K = 2
> **输出:** ababab
> **解释:**
> 用‘a’替换 _ 然后字符串每 2 个字符后会遵循一个重复序列。
> 
> **输入:** S = _b_abc_bc，K = 3
> T3】输出 : abcabcabc

**方法:**这个问题可以通过[迭代字符串 **S** 来解决。](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/)按照以下步骤解决此问题:

*   用**空**字符初始化一个大小为 **K** 的数组 **arr[]** 。
*   [使用变量 **i** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，K-1】**中迭代:
    *   [使用变量 **j** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【I，N-1】**中迭代，增量为 **K** :
        *   如果不是缺少字符，用当前字符填充数组**arr【I】**。
        *   否则，如果字符与数组 **arr[]** 或 **K** 出现模式都不匹配，则返回 **-1** 。
    *   如果数组 **arr[]** 最初具有**空值**值，即没有找到任何 **K** 出现模式，则按字典顺序填充最小字符，即“ **a** ”。
*   初始化一个大小为 **n** 的数组 **ans[]** ，所有值为“ **a** ”。
*   [使用变量 **i** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【0，N】**中迭代，并将 **ans[i]更新为 arr[i%K]**
*   最后，将这个 **ans** 数组转换成字符串并返回这个。

下面是上述方法的实现:

## 蟒蛇 3

```
# Creating function findMissingChar having parameter
# n i.e length of the string
# k is repeating occurrence of character
# s is given string
def findMissingChar(n, k, s):

    # Creating an array arr of size K,
    # initially with NULL values.
    arr = ['']*k

    # Iterate for loop from 0 to k-1.
    for i in range(k):

        # Iterate for loop from i to n
        # with increment of k.
        for j in range(i, n, k):

            # If it is not missing character
        # then fill array arr[i]
        # with current character.
            if s[j] != '_':
                if arr[i] == '':
                    arr[i] = s[j]
                else:
                    # If character is neither matched
                    # with a array or k occurrence pattern
                    # return -1 in this case.
                    if s[j] != arr[i]:
                        return -1

        # If the array having initially null values
        # i.e haven't found any k occurrence pattern
        # then fill lexicographically
        # the smallest character i.e 'a'.
        if arr[i] == '':
            arr[i] = 'a'

    # Creating ans array having size n
    # and initialize with 'a'.     
    ans = ['a']*n

    # Filling ans array with suitable
    # lexicographically smallest character.
    for i in range(n):
        ans[i] = arr[i % k]
    return ''.join(ans)

# Driver Code   
s = '_b_abc_bc'
n = len(s)
k = 3
print(findMissingChar(n, k, s))
```

**Output:** 

```
abcabcabc
```

***时间复杂度:** O(N*K)*

***辅助空间:** O(N)*