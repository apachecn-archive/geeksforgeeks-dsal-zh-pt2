# 数字的不同排列

> 原文:[https://www . geesforgeks . org/distinct-排列一个数字/](https://www.geeksforgeeks.org/distinct-permutations-of-a-number/)

给定一个整数 **N** ，任务是打印数字 **N** 的所有不同排列。

**示例:**

> **输入:** N = 133
> **输出:** 133 313 3 31
> **说明:**
> 共有 6 种排列，分别为【133，313，331，133，313，331】。
> 在所有这些排列中，不同的排列是[133，313，331]。
> 
> **输入:**N = 7668
> T3】输出:7668 7686 7866 6768 6786 6678 6687 6876 6867 8766 8667

**方法:**按照以下步骤解决问题:

*   初始化一个空的[字符串](https://www.geeksforgeeks.org/python-strings/)来存储 **N** 的[等价字符串表示。](https://www.geeksforgeeks.org/type-conversion-python/)
*   初始化一个[映射](https://www.geeksforgeeks.org/python-map-function/)将字符串的每个字符转换成一个整数并存储为一个列表。
*   使用内置 python 函数 [itertools 对该列表进行置换。排列()](https://www.geeksforgeeks.org/permutation-and-combination-in-python/)。
*   初始化另一个列表，说**新列表。**
*   遍历列表的排列，如果排列(列表)不在**新列表**中，则将该列表附加到**新列表**中。
*   初始化一个空字符串，**s = "**另一个空列表说 **permuteList。**
*   [遍历列表](https://www.geeksforgeeks.org/iterate-over-a-list-in-python/) **新建列表**，并对每个列表执行以下操作:
    *   [遍历列表](https://www.geeksforgeeks.org/iterate-over-a-list-in-python/)并将每个元素添加到字符串 **s** 中。
    *   遍历后，[将字符串转换为整数](https://www.geeksforgeeks.org/convert-string-to-integer-in-python/)。
    *   将该整数追加到**允许列表**中。
*   打印**置换列表**的值，作为可能的不同置换。

下面是上述方法的实现:

## 蟒蛇 3

```
# Python3 program for the above approach

from itertools import permutations

# Utility function to print
# all distinct permutations
def uniquePermutationsUtil(permute):

    p = []

    # Traverse the list permute[]
    for i in permute:

        # Convert this permutation to list
        permutelist = list(i)

        # Append this list to p
        p.append(permutelist)

    # Stores unique permutations
    newlist = []

    # Traverse list p[]
    for i in p:

        # If permutation is
        # not in newlist
        if i not in newlist:
            newlist.append(i)

    # Initialize empty list
    permutelist = []

    # Traverse the list newlist[]
    for i in newlist:

        # Initialize empty string
        s = ""

        # Traversing in element list
        for j in i:

            # Convert each
            # element to string
            s = s + str(j)

        # Convert string to integer
        s = int(s)

        # Append the unique
        # permutation to permutelist
        permutelist.append(s)

    # Print all distinct permutations
    print(*permutelist)

# Function to print all
# distinct permutations
def uniquePermutations(N):

    # Stores equivalent string
    # representation of N
    num = str(N)

    # Convert each character to
    # integer and store in the list
    lis = list(map(int, num))

    # Built in method to store all
    # permutations of the list
    permute = permutations(lis)

    # Print unique permutations
    uniquePermutationsUtil(permute)

# Driver Code

# Given value of N
N = 7668

# Function call to find all
# distinct permutations of N
uniquePermutations(N)
```

**Output:** 

```
7668 7686 7866 6768 6786 6678 6687 6876 6867 8766 8676 8667
```

***时间复杂度:** O(N * N！)*
***辅助空间:** O(N * N！)*