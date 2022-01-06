# 仅将二进制字符串转换为 0 所需的翻转字符的最小成本

> 原文:[https://www . geesforgeks . org/最小翻转字符成本-仅需要将二进制字符串转换为 0s/](https://www.geeksforgeeks.org/minimum-cost-of-flipping-characters-required-to-convert-binary-string-to-0s-only/)

给定[二进制字符串](https://www.geeksforgeeks.org/tag/binary-string/) **str** ，以及整数 **A** ，表示将连续 **1** s 转换为 **0** s 的成本，以及 **B** ，表示将 **0** s 转换为 **1** s 的成本，任务是找到**最小成本**将字符串 **str** 缩减为

****示例:****

> ****输入:** str = "01101110 "，A = 5，B = 1
> **输出:** 6
> **解释:**
> 将 str[3]转换为**‘1’**。成本= 1，str = "01111110 "。
> 将子串{str[1]，… str[6]}转换为 **'0'** 。成本= 5，str = "00000000 "。**
> 
> ****输入:** str = "1010010011110111 "，A = 12，B = 14
> T3】输出: 60**

****方法:**给定的问题可以基于以下观察来解决:**

> **对于**1**s**【L1、R1】**和**【L2、R2】**(其中 **L2 > R1** )的任意一对连续分段，选择将这两个分段转换为 **0** s，费用为 **2 * A** 或将这两个分段之间的 **0** s 转换为 **1** s 并转换**【L1，R2】****

**按照以下步骤解决问题:**

*   **初始化变量 **left_1** 并将**最左边的‘1’**的索引存储在**字符串**中**
*   **初始化另一个变量 **right_1** ，并将**最右边的‘1’**的索引存储在**字符串**中。**
*   **如果 **left_1** 和 **right_1** 不存在，那么 **str** 已经只包含 **0** s。因此，打印 **0** 作为最小成本**
*   **否则，**串**中至少有一个**‘1’**。因此，初始化**成本= A** 。**
*   **[用指针 **i** 遍历字符串](https://www.geeksforgeeks.org/iterate-over-characters-of-a-string-in-python/) **字符串**中从**左 _1** 到**右 _1** 的字符

    *   计算 **i** 右侧连续 **0** s 的数量，并将其存储在变量**零**中。
    *   如果**零点**的长度超过 **0** ，将 **0** s 转换为 **1** s 的费用为**零点* B** 或将连续的 **1** s 转换为 **0** s 的费用为 **A** 。
    *   因此，将**成本**增加**分钟(零*乙，甲)**** 
*   **最后，打印获得的最小成本。**

**下面是上述方法的实现:**

## **C++**

```
// C++ Program to implement
// the above approach
#include <iostream>
using namespace std;

// Function to find the minimum cost
// to convert given string to 0s only
void convert_to_allzeroes(string str,
                          int a, int b)
{
    // Length of string
    int len = str.length();

    // Stores the index of leftmost '1' in str
    int left_1, i = 0;

    while (i < len && str[i] == '0')
        i++;

    // Update the index of leftmost '1' in str
    left_1 = i;

    // Stores the index of rightmost '1' in str
    int right_1;
    i = len - 1;
    while (i >= 0 && str[i] == '0')
        i--;

    // Update the index of rightmost '1' in str
    right_1 = i;

    // If str does not contain any '1's
    if (left_1 == len && right_1 == -1) {

        // No changes required
        cout << 0;
        return;
    }

    // Stores minimum cost
    int cost = a, zeroes;

    // Iterating through str form
    // left_1 to right_1
    for (i = left_1; i <= right_1; i++) {

        // Stores length of
        // consecutive 0s
        zeroes = 0;

        // Calculate length of consecutive 0s
        while (i < len && str[i] == '0') {

            zeroes++;
            i++;
        }

        // If a substring of 0s exists
        if (zeroes)

            // Update minimum cost
            cost += min(zeroes * b, a);
    }
    // Printing the minimum cost
    cout << cost;
}

// Driver Code
int main()
{
    string str = "01101110";
    int A = 5, B = 1;
    convert_to_allzeroes(str, A, B);
    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program to implement
// the above approach
class GFG{

// Function to find the minimum cost
// to convert given string to 0s only
public static void convert_to_allzeroes(String str,
                                        int a, int b)
{

    // Length of string
    int len = str.length();

    // Stores the index of leftmost '1' in str
    int left_1, i = 0;

    while (i < len && str.charAt(i) == '0')
        i++;

    // Update the index of leftmost '1' in str
    left_1 = i;

    // Stores the index of rightmost '1' in str
    int right_1;
    i = len - 1;

    while (i >= 0 && str.charAt(i) == '0')
        i--;

    // Update the index of rightmost '1' in str
    right_1 = i;

    // If str does not contain any '1's
    if (left_1 == len && right_1 == -1)
    {

        // No changes required
        System.out.print(0);
        return;
    }

    // Stores minimum cost
    int cost = a, zeroes;

    // Iterating through str form
    // left_1 to right_1
    for(i = left_1; i <= right_1; i++)
    {

        // Stores length of
        // consecutive 0s
        zeroes = 0;

        // Calculate length of consecutive 0s
        while (i < len && str.charAt(i) == '0')
        {
            zeroes++;
            i++;
        }

        // If a substring of 0s exists
        if (zeroes != 0)

            // Update minimum cost
            cost += Math.min(zeroes * b, a);
    }

    // Printing the minimum cost
    System.out.print(cost);
}

// Driver code
public static void main(String[] args)
{
    String str = "01101110";
    int A = 5, B = 1;

    convert_to_allzeroes(str, A, B);
}
}

// This code is contributed by divyeshrabadiya07
```

## **蟒蛇 3**

```
# Python3 Program to implement
# the above approach

# Function to find the minimum
# cost to convert given string
# to 0s only
def convert_to_allzeroes(st,
                         a, b):

    # Length of string
    length = len(st)

    # Stores the index of
    # leftmost '1' in str
    left_1 = 0
    i = 0

    while (i < length and
           st[i] == '0'):
        i += 1

    # Update the index of
    # leftmost '1' in str
    left_1 = i

    # Stores the index of
    # rightmost '1' in str
    right_1 = 0
    i = length - 1

    while (i >= 0 and
           st[i] == '0'):
        i -= 1

    # Update the index of
    # rightmost '1' in str
    right_1 = i

    # If str does not contain
    # any '1's
    if (left_1 == length and
        right_1 == -1):

        # No changes required
        print(0)
        return

    # Stores minimum cost
    cost = a

    # Iterating through str form
    # left_1 to right_1
    for i in range(left_1,
                   right_1 + 1):

        # Stores length of
        # consecutive 0s
        zeroes = 0

        # Calculate length of
        # consecutive 0s
        while (i < length and
               st[i] == '0'):
            zeroes += 1
            i += 1

        # If a substring of
        # 0s exists
        if (zeroes):

            # Update minimum cost
            cost += min(zeroes * b, a)

    # Printing the minimum cost
    print(cost)

# Driver Code
if __name__ == "__main__":

    st = "01101110"
    A = 5
    B = 1
    convert_to_allzeroes(st, A, B)

# This code is contributed by Chitranayal
```

## **C#**

```
// C# program to implement
// the above approach 
using System;

class GFG{

// Function to find the minimum cost
// to convert given string to 0s only
public static void convert_to_allzeroes(string str,
                                        int a, int b)
{

    // Length of string
    int len = str.Length;

    // Stores the index of leftmost '1' in str
    int left_1, i = 0;

    while (i < len && str[i] == '0')
        i++;

    // Update the index of leftmost '1' in str
    left_1 = i;

    // Stores the index of rightmost '1' in str
    int right_1;
    i = len - 1;

    while (i >= 0 && str[i] == '0')
        i--;

    // Update the index of rightmost '1' in str
    right_1 = i;

    // If str does not contain any '1's
    if (left_1 == len && right_1 == -1)
    {

        // No changes required
        Console.Write(0);
        return;
    }

    // Stores minimum cost
    int cost = a, zeroes;

    // Iterating through str form
    // left_1 to right_1
    for(i = left_1; i <= right_1; i++)
    {

        // Stores length of
        // consecutive 0s
        zeroes = 0;

        // Calculate length of consecutive 0s
        while (i < len && str[i] == '0')
        {
            zeroes++;
            i++;
        }

        // If a substring of 0s exists
        if (zeroes != 0)

            // Update minimum cost
            cost += Math.Min(zeroes * b, a);
    }

    // Printing the minimum cost
    Console.Write(cost);
}

// Driver code
public static void Main()
{
    string str = "01101110";
    int A = 5, B = 1;

    convert_to_allzeroes(str, A, B);
}
}

// This code is contributed by susmitakundugoaldanga
```

## **java 描述语言**

```
<script>

// JavaScript program for the above approach

// Function to find the minimum cost
// to convert given string to 0s only
function convert_to_allzeroes(str, a, b)
{

    // Length of string
    let len = str.length;

    // Stores the index of leftmost '1' in str
    let left_1, i = 0;

    while (i < len && str[i] == '0')
        i++;

    // Update the index of leftmost '1' in str
    left_1 = i;

    // Stores the index of rightmost '1' in str
    let right_1;
    i = len - 1;

    while (i >= 0 && str[i] == '0')
        i--;

    // Update the index of rightmost '1' in str
    right_1 = i;

    // If str does not contain any '1's
    if (left_1 == len && right_1 == -1)
    {

        // No changes required
        document.write(0);
        return;
    }

    // Stores minimum cost
    let cost = a, zeroes;

    // Iterating through str form
    // left_1 to right_1
    for(i = left_1; i <= right_1; i++)
    {

        // Stores length of
        // consecutive 0s
        zeroes = 0;

        // Calculate length of consecutive 0s
        while (i < len && str[i] == '0')
        {
            zeroes++;
            i++;
        }

        // If a substring of 0s exists
        if (zeroes != 0)

            // Update minimum cost
            cost += Math.min(zeroes * b, a);
    }

    // Printing the minimum cost
    document.write(cost);
}

// Driver Code

    let str = "01101110";
    let A = 5, B = 1;

    convert_to_allzeroes(str, A, B);

</script>
```

****Output:** 

```
6
```** 

*****时间复杂度:** O(N)，其中 N 是字符串的长度。*
***辅助空间:** O(1)***