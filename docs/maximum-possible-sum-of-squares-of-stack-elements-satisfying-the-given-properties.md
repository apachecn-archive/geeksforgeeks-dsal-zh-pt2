# 满足给定属性的堆叠元素的最大可能平方和

> 原文:[https://www . geeksforgeeks . org/满足给定属性的堆栈元素的最大可能平方和/](https://www.geeksforgeeks.org/maximum-possible-sum-of-squares-of-stack-elements-satisfying-the-given-properties/)

给定两个整数 **S** 和 **N、**，任务是找到 **N** 个整数的最大可能平方和，这些整数可以放入[堆栈](https://www.geeksforgeeks.org/stack-data-structure/)中，从而满足以下属性:

*   堆栈顶部的整数不应小于紧接其下的元素。
*   所有**叠加**元素应该在**【1，9】**范围内。
*   堆栈元素的总和应该正好等于 **S** 。

如果无法获得这样的排列，打印 **-1** 。

**示例:**

> **输入:** S = 12，N = 3
> **输出:** 86
> **说明:**
> 堆栈排列【9，2，1】生成和 12 (= S)，从而满足属性。
> 因此，最大可能平方和= 9 * 9 + 2 * 2 + 1 * 1= 81 + 4 + 1 = 86
> 
> **输入:** S = 11，N = 1
> **输出:** -1

**方法:**按照以下步骤解决问题:

1.  检查 **S** 是否有效，即是否在**【N，9 * N】**范围内。
2.  初始化一个变量，比如 **res** 来存储堆栈元素的最大平方和。
3.  堆栈中整数的最小值可以是 1，因此用 1 初始化所有堆栈元素。因此，从 **S** 中扣除 **N** 。
4.  现在，检查大于 1 的整数个数。为此，从堆栈底部开始向整数添加 8(如果可能)，并继续添加，直到 **S > 0** 。
5.  最后，将 **S % 8** 加入到当前整数中，并用 1 填充所有剩余的堆栈元素。
6.  最后，加上堆栈元素的平方和。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the maximum
// sum of squares of stack elements
void maxSumOfSquares(int N,
                     int S)
{
  // Stores the sum ofsquares
  // of stack elements
  int res = 0;

  // Check if sum is valid
  if (S < N || S > 9 * N)
  {
    cout << (-1);
    return;
  }

  // Initialize all stack
  // elements with 1
  S = S - N;

  // Stores the count the
  // number of stack elements
  // not equal to 1
  int c = 0;

  // Add the sum of squares
  // of stack elements not
  // equal to 1
  while (S > 0)
  {
    c++;
    if (S / 8 > 0)
    {
      res += 9 * 9;
      S -= 8;
    }
    else
    {
      res += (S + 1) *
             (S + 1);
      break;
    }
  }

  // Add 1 * 1 to res as the
  // remaining stack elements
  // are 1
  res = res + (N - c);

  // Print the result
  cout << (res);
}

// Driver Code
int main()
{
  int N = 3;
  int S = 12;

  // Function call
  maxSumOfSquares(N, S);
}
// This code is contributed by 29AjayKumar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.io.*;
import java.util.*;

class GFG {

    // Function to find the maximum
    // sum of squares of stack elements
    public static void maxSumOfSquares(
        int N, int S)
    {
        // Stores the sum ofsquares
        // of stack elements
        int res = 0;

        // Check if sum is valid
        if (S < N || S > 9 * N) {

            System.out.println(-1);
            return;
        }

        // Initialize all stack
        // elements with 1
        S = S - N;

        // Stores the count the
        // number of stack elements
        // not equal to 1
        int c = 0;

        // Add the sum of squares of
        // stack elements not equal to 1
        while (S > 0) {
            c++;

            if (S / 8 > 0) {

                res += 9 * 9;
                S -= 8;
            }

            else {

                res += (S + 1)
                       * (S + 1);
                break;
            }
        }

        // Add 1 * 1 to res as the
        // remaining stack elements are 1
        res = res + (N - c);

        // Print the result
        System.out.println(res);
    }

    // Driver Code
    public static void main(String args[])
    {
        int N = 3;
        int S = 12;

        // Function call
        maxSumOfSquares(N, S);
    }
}
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find the maximum
# sum of squares of stack elements
def maxSumOfSquares(N, S):

    # Stores the sum ofsquares
    # of stack elements
    res = 0

    # Check if sum is valid
    if (S < N or S > 9 * N):
        cout << -1;
        return

    # Initialize all stack
    # elements with 1
    S = S - N

    # Stores the count the
    # number of stack elements
    # not equal to 1
    c = 0

    # Add the sum of squares of
    # stack elements not equal to 1
    while (S > 0):
        c += 1

        if (S // 8 > 0):
            res += 9 * 9
            S -= 8
        else:
            res += (S + 1) * (S + 1)
            break

    # Add 1 * 1 to res as the
    # remaining stack elements are 1
    res = res + (N - c)

    # Print the result
    print(res)

# Driver Code
if __name__ == '__main__':

    N = 3
    S = 12

    # Function call
    maxSumOfSquares(N, S)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG{

// Function to find the maximum
// sum of squares of stack elements
public static void maxSumOfSquares(int N,
                                   int S)
{
  // Stores the sum ofsquares
  // of stack elements
  int res = 0;

  // Check if sum is valid
  if (S < N || S > 9 * N)
  {
    Console.WriteLine(-1);
    return;
  }

  // Initialize all stack
  // elements with 1
  S = S - N;

  // Stores the count the
  // number of stack elements
  // not equal to 1
  int c = 0;

  // Add the sum of squares of
  // stack elements not equal to 1
  while (S > 0)
  {
    c++;

    if (S / 8 > 0)
    {
      res += 9 * 9;
      S -= 8;
    }

    else
    {
      res += (S + 1) *
             (S + 1);
      break;
    }
  }

  // Add 1 * 1 to res
  // as the remaining
  // stack elements are 1
  res = res + (N - c);

  // Print the result
  Console.WriteLine(res);
}

// Driver Code
public static void Main(String []args)
{
  int N = 3;
  int S = 12;

  // Function call
  maxSumOfSquares(N, S);
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>
// javascript program to implement
// the above approach   
// Function to find the maximum
    // sum of squares of stack elements
    function maxSumOfSquares(N , S) {
        // Stores the sum ofsquares
        // of stack elements
        var res = 0;

        // Check if sum is valid
        if (S < N || S > 9 * N) {

            document.write(-1);
            return;
        }

        // Initialize all stack
        // elements with 1
        S = S - N;

        // Stores the count the
        // number of stack elements
        // not equal to 1
        var c = 0;

        // Add the sum of squares of
        // stack elements not equal to 1
        while (S > 0) {
            c++;

            if (parseInt(S / 8) > 0) {

                res += 9 * 9;
                S -= 8;
            }

            else {

                res += (S + 1) * (S + 1);
                break;
            }
        }

        // Add 1 * 1 to res as the
        // remaining stack elements are 1
        res = res + (N - c);

        // Print the result
        document.write(res);
    }

    // Driver Code

        var N = 3;
        var S = 12;

        // Function call
        maxSumOfSquares(N, S);

// This code contributed by aashish1995
</script>
```

**Output:** 

```
86
```

***时间复杂度** : O(N)*
***辅助空间:** O(1)*