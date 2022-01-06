# 用给定的位“或”和位“异或”值找到所有可能的对

> 原文:[https://www . geeksforgeeks . org/find-所有可能的对与给定的按位或与按位异或值/](https://www.geeksforgeeks.org/find-all-possible-pairs-with-given-bitwise-or-and-bitwise-xor-values/)

给定两个正整数 **A** 和 **B** 表示两个正整数的[按位异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)和[按位或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)，任务是找到所有可能的对 **(x，y)** ，使得 **x ^ y** 等于 **A** 和 **x | y** 等于 **B** 。

**示例:**

> **输入:** A = 5，B = 7
> **输出:**
> 2 7
> 3 6
> 6 3
> 7 2
> **解释:**
> 7(异或)2 = 5 和 7(或)2 = 7
> 3(异或)6 = 5 和 3(或)6 = 7
> 
> **输入:** A = 8，B = 10
> T3】输出:T5】2 10
> 10 2

**天真方法:**解决问题最简单的方法是生成所有可能的对，对于每一对，检查它们的按位异或和按位或是否分别等于 **A** 和 **B** 。

**时间复杂度:**O(B<sup>2</sup>)
T5】辅助空间: O(1)

**有效方法:**思路是遍历 **x** 的所有可能值，并使用 XOR 的**属性，即如果 **x ^ y = A** ，那么 **x ^ A = y** 找到 **y** 的所有可能值。按照以下步骤解决问题:**

*   使用变量从 **1** 迭代到 **B** ，比如说 **i** ，执行以下操作:
    *   将变量 **y** 初始化为 **i ^ A** 。
    *   检查 **y** 的值是否大于 **0** 、 **(i | y)** 是否等于 **B** 。
    *   如果发现为真，则打印 **i** 和 **y** 的值。

下面是上述方法的实现:

## C++

```
// C++ code for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find pairs with
// XOR equal to A and OR equal to B
void findPairs(int A, int B)
{
    // Iterate from 1 to B
    for (int i = 1; i <= B; i++) {
        int y = A ^ i;

        // Check if (i OR y) is B
        if (y > 0 and (i | y) == B) {
            cout << i << " " << y << endl;
        }
    }
}

// Driver Code
int main()
{
    int A = 8, B = 10;

    findPairs(A, B);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for the above approach
import java.util.*;

class GFG{

// Function to find pairs with
// XOR equal to A and OR equal to B
static void findPairs(int A, int B)
{

    // Iterate from 1 to B
    for(int i = 1; i <= B; i++)
    {
        int y = A ^ i;

        // Check if (i OR y) is B
        if (y > 0 && (i | y) == B)
        {
            System.out.println(i + " " + y);
        }
    }
}

// Driver Code
public static void main(String[] args)
{
    int A = 8, B = 10;

    findPairs(A, B);
}
}

// This code is contributed by Hritik
```

## 蟒蛇 3

```
# Python3 code for the above approach

# Function to find pairs with
# XOR equal to A and OR equal to B
def findPairs(A, B):

    # Iterate from 1 to B
    for i in range(1, B + 1):

        y = A ^ i

        # Check if (i OR y) is B
        if (y > 0 and (i | y) == B):
            print(i, " ", y)

# Driver Code
A = 8
B = 10

findPairs(A, B)

# This code is contributed by amreshkumar3
```

## C#

```
// C# code for the above approach
using System;
class GFG
{

    // Function to find pairs with
    // XOR equal to A and OR equal to B
    static void findPairs(int A, int B)
    {

        // Iterate from 1 to B
        for(int i = 1; i <= B; i++)
        {
            int y = A ^ i;

            // Check if (i OR y) is B
            if (y > 0 && (i | y) == B)
            {
                Console.WriteLine(i + " " + y);
            }
        }
    }

  // Driver code
  static void Main ()
  {
    int A = 8, B = 10;

    findPairs(A, B);
  }
}

// This code is contributed by suresh07.
```

## java 描述语言

```
<script>

// JavaScript code for the above approach

// Function to find pairs with
// XOR equal to A and OR equal to B
function findPairs(A, B) {
    // Iterate from 1 to B
    for (let i = 1; i <= B; i++) {
        let y = A ^ i;

        // Check if (i OR y) is B
        if (y > 0 && (i | y) == B) {
            document.write(i + " " + y + "<br>");
        }
    }
}

// Driver Code

let A = 8, B = 10;

findPairs(A, B);

// This code is contributed by gfgking

</script>
```

**Output:** 

```
2 10
10 2
```

***时间复杂度:** O(B)*
***辅助空间:** O(1)*