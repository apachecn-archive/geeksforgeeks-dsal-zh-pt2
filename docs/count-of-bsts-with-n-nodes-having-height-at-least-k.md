# 高度至少为 K 的 N 个节点的 BST 计数

> 原文:[https://www . geeksforgeeks . org/count-of-bsts-with-n-nodes-with-height-at-k/](https://www.geeksforgeeks.org/count-of-bsts-with-n-nodes-having-height-at-least-k/)

给定两个正整数 **N** 和 **K** ，任务是找到高度大于或等于 **K** 的 [**二分搜索法树**](https://www.geeksforgeeks.org/binary-search-tree-data-structure/) (BST)节点数。

**注**:这里的高度是指 BST 的最大深度。

**示例**:

> **输入** : N = 3，K = 3
> **输出** : 4
> **说明** :
> 高度大于等于 K 的二分搜索法树有 4 种可能
> 
> 1 1 3 3
> \ \//
> 2 3 2 1
> \ |/\
> 3 2 1 2
> 
> **输入** : N = 4，K = 2
> **输出** : 14

**逼近**:这个问题可以用[递归](https://www.geeksforgeeks.org/recursion/)解决。按照以下步骤解决问题:

*   **基本情况:**如果 **N** 等于 **1** 则返回 **1** 。
*   初始化一个变量**计数**为 **0** 来存储有效[计数](https://www.geeksforgeeks.org/construct-all-possible-bsts-for-keys-1-to-n/)的数量。
*   [使用变量 **i:** 在范围](https://www.geeksforgeeks.org/range-based-loop-c/)**【1，N】**中迭代
    *   如果**I-1****N-I**大于等于 **K** ，则:
        *   [递归调用](https://www.geeksforgeeks.org/recursive-functions/)左子树的函数，其中**节点**为**I–1****高度为 K–1**，将找到创建左子树**的方法数。**
        *   [递归调用](https://www.geeksforgeeks.org/recursive-functions/)右子树函数，节点**为**N–I**，高度**为**K–1**，找到创建右子树的方法。****
    *   在 **countBsts 中添加结果。**
*   完成上述步骤后，打印**计数表。**

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the number of BST's
// with N nodes of height greater than
// or equal to K
int numOfBst(int n, int k)
{

    if (n <= 1) {
        return 1;
    }

    // Store number of valid BSTs
    int countBsts = 0;

    // Traverse from 1 to n
    for (int i = 1; i <= n; i++) {
        // If Binary Tree with height greater
        // than K exist
        if (i - 1 >= k or n - i >= k)
            countBsts
 += numOfBst(i - 1, k - 1)
 * numOfBst(n - i, k - 1);
    }

    // Finally, return the countBsts
    return countBsts;
}
// Driver Code
int main()
{

    // Given Input
    int n = 4;
    int k = 2;

    // Function call to find the number
    // of BSTs greater than k
    cout << numOfBst(n, k - 1) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG
{

  // Function to find the number of BST's
  // with N nodes of height greater than
  // or equal to K
  static int numOfBst(int n, int k)
  {

    if (n <= 1) {
      return 1;
    }

    // Store number of valid BSTs
    int countBsts = 0;

    // Traverse from 1 to n
    for (int i = 1; i <= n; i++)
    {

      // If Binary Tree with height greater
      // than K exist
      if (i - 1 >= k || n - i >= k)
        countBsts += numOfBst(i - 1, k - 1)
        * numOfBst(n - i, k - 1);
    }

    // Finally, return the countBsts
    return countBsts;
  }

  // Driver Code
  public static void main(String[] args)
  {

    // Given Input
    int n = 4;
    int k = 2;

    // Function call to find the number
    // of BSTs greater than k
    System.out.println(numOfBst(n, k - 1));

  }
}

// This code is contributed by potta lokesh.
```

## 蟒蛇 3

```
# python 3 program for the above approach

# Function to find the number of BST's
# with N nodes of height greater than
# or equal to K
def numOfBst(n, k):
    if (n <= 1):
        return 1

    # Store number of valid BSTs
    countBsts = 0

    # Traverse from 1 to n
    for i in range(1, n + 1, 1):

        # If Binary Tree with height greater
        # than K exist
        if (i - 1 >= k or n - i >= k):
            countBsts += numOfBst(i - 1, k - 1) * numOfBst(n - i, k - 1)

    # Finally, return the countBsts
    return countBsts

# Driver Code
if __name__ == '__main__':
    # Given Input
    n = 4
    k = 2

    # Function call to find the number
    # of BSTs greater than k
    print(numOfBst(n, k - 1))

    # This code is contributed by bgangwar59.
```

## C#

```
// C# program for the above approach
using System;
class GFG {

  // Function to find the number of BST's
  // with N nodes of height greater than
  // or equal to K
  static int numOfBst(int n, int k)
  {

    if (n <= 1) {
      return 1;
    }

    // Store number of valid BSTs
    int countBsts = 0;

    // Traverse from 1 to n
    for (int i = 1; i <= n; i++)
    {

      // If Binary Tree with height greater
      // than K exist
      if (i - 1 >= k || n - i >= k)
        countBsts += numOfBst(i - 1, k - 1)
        * numOfBst(n - i, k - 1);
    }

    // Finally, return the countBsts
    return countBsts;
  }

  // Driver code
  static void Main()
  {

    // Given Input
    int n = 4;
    int k = 2;

    // Function call to find the number
    // of BSTs greater than k
    Console.WriteLine(numOfBst(n, k - 1));
  }
}

// This code is contributed by divyeshrabadiya07.
```

## java 描述语言

```
<script>
        // JavaScript program for the above approach

        // Function to find the number of BST's
        // with N nodes of height greater than
        // or equal to K
        function numOfBst(n, k) {

            if (n <= 1) {
                return 1;
            }

            // Store number of valid BSTs
            let countBsts = 0;

            // Traverse from 1 to n
            for (let i = 1; i <= n; i++) {
                // If Binary Tree with height greater
                // than K exist
                if (i - 1 >= k || n - i >= k)
                    countBsts
                        += numOfBst(i - 1, k - 1)
                        * numOfBst(n - i, k - 1);
            }

            // Finally, return the countBsts
            return countBsts;
        }
        // Driver Code

        // Given Input
        let n = 4;
        let k = 2;

        // Function call to find the number
        // of BSTs greater than k
        document.write(numOfBst(n, k - 1) + "<br>");

    // This code is contributed by Potta Lokesh

    </script>
```

**Output:** 

```
14
```

***时间复杂度:**O(2<sup>n</sup>)*
***辅助空间:** O(1)*