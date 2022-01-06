# 最多改变一位数字就可以得到的可被 3 整除的不同数字的计数

> 原文:[https://www . geeksforgeeks . org/异数计数-最多可通过改变一位数字获得的 3 整除数/](https://www.geeksforgeeks.org/count-of-different-numbers-divisible-by-3-that-can-be-obtained-by-changing-at-most-one-digit/)

给定一个[串](https://www.geeksforgeeks.org/category/data-structures/c-strings/) **串【】**数 **N，**任务是通过最多改变给定数的一个数字来计算使给定数可被 3 整除的方法数。

**示例:**

> **输入:**str[]=“23”
> **输出:** 7
> **说明:**下面是可以由 3–03，21，24，27，33，63，93
> 1 整除的字符串组成的数字。将 2 改为 0 (0+3)=3 可被 3 整除
> 2。变 3 为 1 (2+1)=3 可被 3 整除
> 3 变 3 为 4 (2+4)=6 可被 3 整除
> 4 变 2 为 3 和是 6 可被 3 整除
> 同样有 7 种方法可以让给定的数被 3 整除
> 
> **输入:**str[]=“235”
> T3】输出: 9

**方法:**解决这个问题的思路很简单。计算给定数字的位数总和，然后对于每个索引，移除该数字并尝试从 **0** 到 **9** 的所有可能的位数，并查看总和是否可被 **3** 整除。按照以下步骤解决问题:

*   将变量**总和**初始化为 **0** 来存储数字的位数总和。
*   [使用变量 **i** 迭代一个范围](https://www.geeksforgeeks.org/loops-in-java/)**【0，N】**，并执行以下步骤:
    *   将变量**总和中第一个**指标的数字值相加。
*   初始化变量**计数**为 **0** 存储答案。
*   [使用变量 **i** 迭代一个范围](https://www.geeksforgeeks.org/loops-in-java/)**【0，N】**，并执行以下步骤:
    *   将变量**剩余 _ 总和**初始化为**总和-(number.charAt(i)-48)。**
    *   [使用变量 **j** 迭代一个范围](https://www.geeksforgeeks.org/loops-in-java/)**【0，9】**，并执行以下步骤:
        *   将 **j** 的值加到变量**剩余 _ 和**上，如果**剩余 _ 和**可以被 **3** 整除，并且 **j** 不等于第**I-第**索引处的数字，那么将**的值加起来，用 **1 计数**。**
*   执行上述步骤后，打印**计数**的值作为答案。

下面是上述方法的实现..

## C++

```
// C++ program fo the above approach
#include<bits/stdc++.h>
using namespace std;

    // Function to count the number of
    // possible numbers divisible by 3
   void findCount(string number)
    {

    // Calculate the sum
    int sum = 0;
    for (int i = 0; i < number.length(); ++i) {
    sum += number[i] - 48;
    }

    // Store the answer
    int count = 0;

    // Iterate over the range
    for (int i = 0; i < number.length(); ++i) {

    // Decreasing the sum
    int remaining_sum
    = sum - (number[i] - 48);

    // Iterate over the range
    for (int j = 0; j <= 9; ++j) {

    // Checking if the new sum
    // is divisible by 3 or not
    if ((remaining_sum + j) % 3 == 0
    && j != number[i] - 48) {

    // If yes increment
    // the value of the count
    ++count;
    }
    }
    }
    cout<<count;
    }

    // Driver Code
   int main()
    {
    // Given number
    string number = "235";

    findCount(number);
    }

// This code is contributed by ipg2016107.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program fo the above approach
import java.io.*;
import java.util.*;

class GFG {

    // Function to count the number of
    // possible numbers divisible by 3
    public static void findCount(String number)
    {

        // Calculate the sum
        int sum = 0;
        for (int i = 0; i < number.length(); ++i) {
            sum += number.charAt(i) - 48;
        }

        // Store the answer
        int count = 0;

        // Iterate over the range
        for (int i = 0; i < number.length(); ++i) {

            // Decreasing the sum
            int remaining_sum
                = sum - (number.charAt(i) - 48);

            // Iterate over the range
            for (int j = 0; j <= 9; ++j) {

                // Checking if the new sum
                // is divisible by 3 or not
                if ((remaining_sum + j) % 3 == 0
                    && j != number.charAt(i) - 48) {

                    // If yes increment
                    // the value of the count
                    ++count;
                }
            }
        }
        System.out.println(count);
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given number
        String number = "235";

        findCount(number);
    }
}
```

## 蟒蛇 3

```
# Python program fo the above approach

# Function to count the number of
# possible numbers divisible by 3
def findCount(number):

    # Calculate the sum
    sum = 0
    for i in range(len(number)):
        sum += int(number[i]) - 48

    # Store the answer
    count = 0

    # Iterate over the range
    for i in range(len(number)):

        # Decreasing the sum
        remaining_sum = sum - (int(number[i]) - 48)

        # Iterate over the range
        for j in range(10):

            # Checking if the new sum
            # is divisible by 3 or not
            if ((remaining_sum + j) % 3 == 0 and j != int(number[i]) - 48):

                # If yes increment
                # the value of the count
                count += 1

    print(count)

# Driver Code

# Given number
number = "235"
findCount(number)

# This code is contributed by gfgking.
```

## C#

```
// C# program fo the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to count the number of
// possible numbers divisible by 3
static void findCount(string number)
{

    // Calculate the sum
    int sum = 0;
    for(int i = 0; i < number.Length; ++i)
    {
        sum += (int)number[i] - 48;
    }

    // Store the answer
    int count = 0;

    // Iterate over the range
    for(int i = 0; i < number.Length; ++i)
    {

        // Decreasing the sum
        int remaining_sum = sum - ((int)number[i] - 48);

        // Iterate over the range
        for(int j = 0; j <= 9; ++j)
        {

            // Checking if the new sum
            // is divisible by 3 or not
            if ((remaining_sum + j) % 3 == 0 &&
                j != number[i] - 48)
            {

                // If yes increment
                // the value of the count
                ++count;
            }
        }
    }
    Console.Write(count);
}

// Driver Code
public static void Main()
{

    // Given number
    string number = "235";

    findCount(number);
}
}

// This code is contributed by SURENDRA_GANGWAR
```

## java 描述语言

```
<script>
// Javascript program fo the above approach

// Function to count the number of
// possible numbers divisible by 3
function findCount(number) {
  // Calculate the sum
  let sum = 0;
  for (let i = 0; i < number.length; ++i) {
    sum += number[i] - 48;
  }

  // Store the answer
  let count = 0;

  // Iterate over the range
  for (let i = 0; i < number.length; ++i) {
    // Decreasing the sum
    let remaining_sum = sum - (number[i] - 48);

    // Iterate over the range
    for (let j = 0; j <= 9; ++j) {
      // Checking if the new sum
      // is divisible by 3 or not
      if ((remaining_sum + j) % 3 == 0 && j != number[i] - 48) {
        // If yes increment
        // the value of the count
        ++count;
      }
    }
  }
  document.write(count);
}

// Driver Code

// Given number
let number = "235";

findCount(number);

// This code is contributed by gfgking

</script>
```

**Output**

```
9
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)