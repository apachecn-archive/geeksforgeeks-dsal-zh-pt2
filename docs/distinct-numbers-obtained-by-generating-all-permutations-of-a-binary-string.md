# 通过生成二进制串的所有排列得到的不同数字

> 原文:[https://www . geesforgeks . org/distinct-numbers-通过生成二进制字符串的所有排列获得/](https://www.geeksforgeeks.org/distinct-numbers-obtained-by-generating-all-permutations-of-a-binary-string/)

给定一个[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **S** ，任务是打印所有不同的十进制数字，这些数字可以通过[生成二进制字符串](https://www.geeksforgeeks.org/permutations-of-a-given-string-using-stl/)的所有排列来获得。

**示例:**

> **输入:** S = "110"
> **输出:** {3，5，6}
> **解释:**
> 所有可能的排列都是{“110”、“101”、“110”、“101”、“011”、“011”}。
> 这些二进制字符串的等价十进制数分别为{6，5，6，5，3，3}。
> 因此，得到的不同十进制数是{3，5，6}。
> 
> **输入:**S = " 1010 "
> T3】输出: {3，5，6，9，10，12}

**方法:**使用[设置](https://www.geeksforgeeks.org/set-in-cpp-stl/)可以解决问题。按照以下步骤解决问题:

*   将给定的[字符串转换为字符列表](https://www.geeksforgeeks.org/python-program-convert-string-list/)。
*   使用内置 python 函数 [itertools 对该列表进行置换。排列()](https://www.geeksforgeeks.org/permutation-and-combination-in-python/)。
*   初始化一个空字符串 **s.**
*   [遍历排列列表](https://www.geeksforgeeks.org/iterate-over-a-list-in-python/#:~:text=In%20Python%2C%20the%20list%20is,over%20a%20list%20in%20Python.)，对每个排列执行以下步骤:
    *   [迭代字符](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/)并将其添加到字符串中。
    *   将此[二进制字符串转换为等效的十进制](https://www.geeksforgeeks.org/program-binary-decimal-conversion/) **。**
    *   [将获得的当前十进制值插入一个集合](https://www.geeksforgeeks.org/set-add-python/)。
*   最后，打印出现在[设置](https://www.geeksforgeeks.org/python-set-method/)中的数字。

下面是上述方法的实现:

## 蟒蛇 3

```
# Python3 program for the above approach

from itertools import permutations

# Function to convert binary
# string to equivalent decimal
def binToDec(n):

    num = n
    dec_value = 0

    # Initializing base
    # value to 1, i.e 2 ^ 0
    base1 = 1

    len1 = len(num)

    for i in range(len1 - 1, -1, -1):

        if (num[i] == '1'):
            dec_value += base1

        base1 = base1 * 2

    # Return the resultant
    # decimal number
    return dec_value

# Function to print all distinct
# decimals represented by the
# all permutations of the string
def printDecimal(permute):

    # Set to store distinct
    # decimal representations
    allDecimals = set()

    # Iterate over all permutations
    for i in permute:

        # Initialize an empty string
        s = ""

        # Traverse the list
        for j in i:

            # Add each element
            # to the string
            s += j

        # Convert the current binary
        # representation to decimal
        result = binToDec(s)

        # Add the current decimal
        # value into the set
        allDecimals.add(result)

    # Print the distinct decimals  
    print(allDecimals)   

# Utility function to print all
# distinct decimal representations
# of all permutations of string
def totalPermutations(string):

    # Convert string to list
    lis = list(string)

    # Built in method to store all
    # the permutations of the list
    permutelist = permutations(lis)

    printDecimal(permutelist)

# Given binary  string
binarystring = '1010'

# Function call to print all distinct
# decimal values represented by all
# permutations of the given string
totalPermutations(binarystring)
```

**Output:** 

```
{3, 5, 6, 9, 10, 12}
```

***时间复杂度:** O(N * N！)*
***辅助空间:** O(N * N！)*