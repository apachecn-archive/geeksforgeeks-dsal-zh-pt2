# 最小化子集加法或乘法，使两个给定的三元组相等

> 原文:[https://www . geeksforgeeks . org/minimum-subset-加法-乘法-使两个给定三元组相等/](https://www.geeksforgeeks.org/minimize-subset-addition-or-multiplication-to-to-make-two-given-triplets-equal/)

给定三个整数 **A、B、C** 表示一个三元组，三个整数 **P、Q、R** 表示另一个三元组。重复选择任意整数，并将其与子集 **(A，B，C)** 中的所有元素相加或相乘，直到两个给定的三元组相等。任务是找到使两个三元组相等所需的最小操作数。

**示例:**

> **输入:** (A，B，C) = (3，4，5)，(P，Q，R) = (6，3，10)
> **输出:** 2
> **解释:**
> **步骤 1:** 将 2 乘以子集{3，5}的所有元素。三元组(A，B，C)变成(6，4，10)。
> **步骤 2:** 将-1 添加到子集{4}。三重态(A，B，C)变为(6，3，10)，与三重态(P，Q，R)相同。
> 因此，所需的最小操作次数为 2 次。
> 
> **输入:** (A，B，C) = (7，6，8)，(p，q，r) = (2，2，2)
> **输出:** 2
> **解释:**
> **第一步:**将子集(7，6，8)的所有元素乘以 0。(A，B，C)修改为(0，0，0)。
> **步骤 2:** 将 2 添加到子集的所有元素(0，0，0)。(A，B，C)修饰成与三元组(P，Q，R)相同的(2，2，2)。
> 因此，所需的最小操作次数为 2 次。

**方法:**按照以下步骤解决给定问题:

*   在每一步中，要么**加**要么**乘**一个整数到三元组的一个子集。该整数可以选择为:
    *   **另外:**在每一步中，尽量固定至少一个数字。因此，对于至少一个 I，需要尝试添加的所有可能数字的集合被限制为**(B[I]–A[I])**
    *   **在乘法中:**遵循相同的逻辑，将 m 乘以一个子集，使得对于至少一个 **i，满足 A[i]*m = B[i]** 。
*   到目前为止，所有操作都有一个基本假设，即在操作之后， **A[i]的至少一个值被转换为 B[i]。**

> 考虑以下情况: **A[]** = [2，3，4]和 **B[]** = [-20，–1，18]
> 上述变换只需两步即可完成，将所有数字乘以 **19** ，然后将 **-58** 加到每个数字上。
> 这种情况必须分开处理。

*   因此，使用[递归](https://www.geeksforgeeks.org/recursion/)来解决处理所有边缘情况的问题，并将为我们提供转换要执行的最小操作数。
*   打印上述步骤后的最小步数。

**以下是上述方法的实现:**

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Utility function to check whether
// given two triplets are equal or not
bool equal(int a[], int b[])
{
    for (int i = 0; i < 3; i++) {
        if (a[i] != b[i]) {
            return false;
        }
    }
    return true;
}

// Utility function to find the number
// to be multiplied such that
// their differences become equal
int mulFac(int a, int b, int c, int d)
{
    if (b != a and (d - c) % (b - a) == 0) {
        return (d - c) / (b - a);
    }
    else {
        return 1;
    }
}

// Function to find minimum operations
void getMinOperations(int a[], int b[],
                      int& ans, int num = 0)
{
    // Base Case
    if (num >= ans)
        return;

    // If triplets are converted
    if (equal(a, b)) {
        ans = min(ans, num);
        return;
    }

    // Maximum possible ans is 3
    if (num >= 2)
        return;

    // Possible values that can be
    // added in next operation
    set<int> add;
    add.insert(b[0] - a[0]);
    add.insert(b[1] - a[1]);
    add.insert(b[2] - a[2]);

    // Possible numbers that we can
    // multiply in next operation
    set<int> mult;
    for (int i = 0; i < 3; i++) {

        // b[i] should be divisible by a[i]
        if (a[i] != 0
            && b[i] % a[i] == 0) {
            mult.insert(b[i] / a[i]);
        }
    }

    // Multiply integer to any 2 numbers
    // such that after multiplication
    // their difference becomes equal
    mult.insert(mulFac(a[0], a[1],
                       b[0], b[1]));
    mult.insert(mulFac(a[2], a[1],
                       b[2], b[1]));
    mult.insert(mulFac(a[0], a[2],
                       b[0], b[2]));
    mult.insert(0);

    // Possible subsets from triplet
    for (int mask = 1; mask <= 7; mask++) {

        // Subset to apply operation
        vector<int> subset;

        for (int j = 0; j < 3; j++)
            if (mask & (1 << j))
                subset.push_back(j);

        // Apply addition on chosen subset
        for (auto x : add) {
            int temp[3];
            for (int j = 0; j < 3; j++)
                temp[j] = a[j];
            for (auto e : subset)
                temp[e] += x;

            // Recursively find all
            // the operations
            getMinOperations(temp, b,
                             ans, num + 1);
        }

        // Applying multiplication
        // on chosen subset
        for (auto x : mult) {

            int temp[3];

            for (int j = 0; j < 3; j++)
                temp[j] = a[j];

            for (auto e : subset)
                temp[e] *= x;

            // Recursively find all
            // the operations
            getMinOperations(temp, b,
                             ans, num + 1);
        }
    }
}

// Driver Code
int main()
{
    // Initial triplet
    int a[] = { 4, 5, 6 };

    // Final Triplet
    int b[] = { 0, 1, 0 };

    // Maximum possible answer = 3
    int ans = 3;

    // Function Call
    getMinOperations(a, b, ans);

    cout << ans << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.util.*;

class GFG{

static int ans_max = 0;

// Utility function to check whether
// given two triplets are equal or not
static boolean equal(int[] a, int[] b)
{
    for(int i = 0; i < 3; i++)
    {
        if (a[i] != b[i])
        {
            return false;
        }
    }
    return true;
}

// Utility function to find the number
// to be multiplied such that
// their differences become equal
static int mulFac(int a, int b,
                  int c, int d)
{
    if (b != a && (d - c) % (b - a) == 0)
    {
        return (d - c) / (b - a);
    }
    else
    {
        return 1;
    }
}

// Function to find minimum operations
static void getMinOperations(int[] a, int[] b,
                             int ans, int num)
{

    // Base Case
    if (num >= ans)
    {
        return;
    }

    // If triplets are converted
    if (equal(a, b))
    {
        ans = Math.min(ans, num);
        ans_max = ans;
        return;
    }

    // Maximum possible ans is 3
    if (num >= 2)
    {
        return;
    }

    // Possible values that can be
    // added in next operation
    Set<Integer> ad = new HashSet<Integer>();
    ad.add(b[0] - a[0]);
    ad.add(b[1] - a[1]);
    ad.add(b[2] - a[2]);

    // Possible numbers that we can
    // multiply in next operation
    Set<Integer> mult = new HashSet<Integer>();
    for(int i = 0; i < 3; i++)
    {

        // b[i] should be divisible by a[i]
        if (a[i] != 0 && b[i] % a[i] == 0)
        {
            mult.add(b[i] / a[i]);
        }
    }

    // Multiply integer to any 2 numbers
    // such that after multiplication
    // their difference becomes equal
    mult.add(mulFac(a[0], a[1],
                    b[0], b[1]));
    mult.add(mulFac(a[2], a[1],
                    b[2], b[1]));
    mult.add(mulFac(a[0], a[2],
                    b[0], b[2]));
    mult.add(0);

    // Possible subsets from triplet
    for(int mask = 1; mask <= 7; mask++)
    {

        // Subset to apply operation
        Vector<Integer> subset = new Vector<Integer>();
        for(int j = 0; j < 3; j++)
        {
            if ((mask & (1 << j)) != 0)
            {
                subset.add(j);
            }
        }

        // Apply addition on chosen subset
        for(int x : ad)
        {
            int[] temp = new int[3];
            for(int j = 0; j < 3; j++)
            {
                temp[j] = a[j];
            }
            for(int e:subset)
            {
                temp[e] += x;
            }

            // Recursively find all
            // the operations
            getMinOperations(temp, b, ans,
                             num + 1);
        }

        // Applying multiplication
        // on chosen subset
        for(int x:mult)
        {
            int[] temp = new int[3];
            for(int j = 0; j < 3; j++)
            {
                temp[j] = a[j];
            }
            for(int e:subset)
            {
                temp[e] *= x;
            }

            // Recursively find all
            // the operations
            getMinOperations(temp, b,
                             ans, num + 1);
        }
    }
}

// Driver Code
public static void main(String[] args)
{

    // Initial triplet
    int[] a = { 4, 5, 6 };

    // Final Triplet
    int[] b = { 0, 1, 0 };

    // Maximum possible answer = 3
    int ans = 3;

    // Function Call
    getMinOperations(a, b, ans, 0);

    System.out.println(ans_max);
}
}

// This code is contributed by avanitrachhadiya2155
```

## 蟒蛇 3

```
# Python3 program for the above approach
ans_max = 0

# Utility function to check whether
# given two triplets are equal or not
def equal(a, b):

    for i in range(3):
        if (a[i] != b[i]):
            return False

    return True

# Utility function to find the number
# to be multiplied such that
# their differences become equal
def mulFac(a, b, c, d):

    if (b != a and (d - c) % (b - a) == 0):
        return (d - c) // (b - a)
    else:
        return 1

# Function to find minimum operations
def getMinOperations(a, b, ans, num):

    global ans_max

    # Base Case
    if (num >= ans):
        return 0

    # If triplets are converted
    if (equal(a, b)):
        ans = min(ans, num)
        ans_max = ans

        return ans

    # Maximum possible ans is 3
    if (num >= 2):
        return 0

    # Possible values that can be
    # added in next operation
    add = {}
    add[(b[0] - a[0])] = 1
    add[(b[1] - a[1])] = 1
    add[(b[2] - a[2])] = 1

    # Possible numbers that we can
    # multiply in next operation
    mult = {}

    for i in range(3):

        # b[i] should be divisible by a[i]
        if (a[i] != 0 and b[i] % a[i] == 0):
            mult[b[i] // a[i]] = 1

    # Multiply integer to any 2 numbers
    # such that after multiplication
    # their difference becomes equal
    mult[mulFac(a[0], a[1], b[0], b[1])] = 1
    mult[mulFac(a[2], a[1], b[2], b[1])] = 1
    mult[mulFac(a[0], a[2], b[0], b[2])] = 1
    mult[0] = 1

    # Possible subsets from triplet
    for mask in range(1, 8):

        # Subset to apply operation
        subset = {}

        for j in range(3):
            if (mask & (1 << j)):
                subset[j] = 1

        # Apply addition on chosen subset
        for x in add:
            temp = [0] * 3
            for j in range(3):
                temp[j] = a[j]
            for e in subset:
                temp[e] += x

            # Recursively find all
            # the operations
            getMinOperations(temp, b, ans,
                             num + 1)

        # Applying multiplication
        # on chosen subset
        for x in mult:
            temp = [0] * 3

            for j in range(3):
                temp[j] = a[j]

            for e in subset:
                temp[e] *= x

            # Recursively find all
            # the operations
            getMinOperations(temp, b, ans,
                             num + 1)

    return ans

# Driver Code
if __name__ == '__main__':

    # Initial triplet
    a = [ 4, 5, 6 ]

    # Final Triplet
    b = [ 0, 1, 0 ]

    # Maximum possible answer = 3
    ans = 3

    # Function Call
    ans = getMinOperations(a, b, ans, 0)

    print(ans_max)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG
{
  static int ans_max = 0;

  // Utility function to check whether
  // given two triplets are equal or not
  static bool equal(int[] a, int[] b)
  {
    for(int i = 0; i < 3; i++)
    {
      if (a[i] != b[i])
      {
        return false;
      }
    }
    return true;
  }

  // Utility function to find the number
  // to be multiplied such that
  // their differences become equal
  static int mulFac(int a, int b,int c, int d)
  {
    if (b != a && (d - c) % (b - a) == 0)
    {
      return (d - c) / (b - a);
    }
    else
    {
      return 1;
    }
  }

  // Function to find minimum operations
  static void getMinOperations(int[] a, int[] b,int ans, int num)
  {

    // Base Case
    if (num >= ans)
    {
      return;
    }

    // If triplets are converted
    if (equal(a, b))
    {
      ans = Math.Min(ans, num);
      ans_max = ans;
      return;
    }

    // Maximum possible ans is 3
    if (num >= 2)
    {
      return;
    }

    // Possible values that can be
    // added in next operation
    HashSet<int> ad = new HashSet<int>();
    ad.Add(b[0] - a[0]);
    ad.Add(b[1] - a[1]);
    ad.Add(b[2] - a[2]);

    // Possible numbers that we can
    // multiply in next operation
    HashSet<int> mult = new HashSet<int>();
    for(int i = 0; i < 3; i++)
    {

      // b[i] should be divisible by a[i]
      if (a[i] != 0 && b[i] % a[i] == 0)
      {
        mult.Add(b[i] / a[i]);

      }

    }

    // Multiply integer to any 2 numbers
    // such that after multiplication
    // their difference becomes equal
    mult.Add(mulFac(a[0], a[1], b[0], b[1]));
    mult.Add(mulFac(a[2], a[1], b[2], b[1]));
    mult.Add(mulFac(a[0], a[2], b[0], b[2]));
    mult.Add(0);

    // Possible subsets from triplet
    for(int mask = 1; mask <= 7; mask++)
    {

      // Subset to apply operation
      List<int> subset=new List<int>();
      for(int j = 0; j < 3; j++)
      {
        if ((mask & (1 << j)) != 0)
        {
          subset.Add(j);
        }
      }

      // Apply addition on chosen subset
      foreach(int x in ad)
      {
        int[] temp = new int[3];
        for(int j = 0; j < 3; j++)
        {
          temp[j] = a[j];
        }
        foreach(int e in subset)
        {
          temp[e] += x;
        }

        // Recursively find all
        // the operations
        getMinOperations(temp, b, ans,num + 1);
      }

      // Applying multiplication
      // on chosen subset
      foreach(int x in mult)
      {
        int[] temp = new int[3];
        for(int j = 0; j < 3; j++)
        {
          temp[j] = a[j];
        }
        foreach(int e in subset)
        {
          temp[e] *= x;
        }

        // Recursively find all
        // the operations
        getMinOperations(temp, b,ans, num + 1);
      }
    }

  }

  // Driver Code
  static public void Main ()
  {

    // Initial triplet
    int[] a = { 4, 5, 6 };

    // Final Triplet
    int[] b = { 0, 1, 0 };

    // Maximum possible answer = 3
    int ans = 3;

    // Function Call
    getMinOperations(a, b, ans, 0);       
    Console.WriteLine(ans_max);
  }
}

// This code is contributed by rag2127
```

## java 描述语言

```
<script>

// Javascript program for the above approach
let ans_max = 0;

// Utility function to check whether
// given two triplets are equal or not
function equal(a, b)
{
    for(let i = 0; i < 3; i++)
    {
        if (a[i] != b[i])
        {
            return false;
        }
    }
    return true;
}

// Utility function to find the number
// to be multiplied such that
// their differences become equal
function mulFac(a, b, c, d)
{
    if (b != a && (d - c) % (b - a) == 0)
    {
        return (d - c) / (b - a);
    }
    else
    {
        return 1;
    }
}

// Function to find minimum operations
function getMinOperations(a, b, ans, num)
{

    // Base Case
    if (num >= ans)
    {
        return;
    }

    // If triplets are converted
    if (equal(a, b))
    {
        ans = Math.min(ans, num);
        ans_max = ans;
        return;
    }

    // Maximum possible ans is 3
    if (num >= 2)
    {
        return;
    }

    // Possible values that can be
    // added in next operation
    let ad = new Set();
    ad.add(b[0] - a[0]);
    ad.add(b[1] - a[1]);
    ad.add(b[2] - a[2]);

    // Possible numbers that we can
    // multiply in next operation
    let mult = new Set();
    for(let i = 0; i < 3; i++)
    {

        // b[i] should be divisible by a[i]
        if (a[i] != 0 && b[i] % a[i] == 0)
        {
            mult.add(b[i] / a[i]);
        }
    }

    // Multiply integer to any 2 numbers
    // such that after multiplication
    // their difference becomes equal
    mult.add(mulFac(a[0], a[1],
                    b[0], b[1]));
    mult.add(mulFac(a[2], a[1],
                    b[2], b[1]));
    mult.add(mulFac(a[0], a[2],
                    b[0], b[2]));
    mult.add(0);

    // Possible subsets from triplet
    for(let mask = 1; mask <= 7; mask++)
    {

        // Subset to apply operation
        let subset = [];
        for(let j = 0; j < 3; j++)
        {
            if ((mask & (1 << j)) != 0)
            {
                subset.push(j);
            }
        }

        // Apply addition on chosen subset
        for(let x of ad.values())
        {
            let temp = new Array(3);
            for(let j = 0; j < 3; j++)
            {
                temp[j] = a[j];
            }
            for(let e = 0; e < subset.length; e++)
            {
                temp[subset[e]] += x;
            }

            // Recursively find all
            // the operations
            getMinOperations(temp, b, ans,
                             num + 1);
        }

        // Applying multiplication
        // on chosen subset
        for(let x of mult.values())
        {
            let temp = new Array(3);
            for(let j = 0; j < 3; j++)
            {
                temp[j] = a[j];
            }
            for(let e = 0; e < subset.length; e++)
            {
                temp[subset[e]] *= x;
            }

            // Recursively find all
            // the operations
            getMinOperations(temp, b,
                             ans, num + 1);
        }
    }
}

// Driver Code
let a = [ 4, 5, 6 ];
let b = [ 0, 1, 0 ];
let ans = 3;

// Function Call
getMinOperations(a, b, ans, 0);

document.write(ans_max);

// This code is contributed by unknown2108

</script>
```

**Output: **

```
2
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)