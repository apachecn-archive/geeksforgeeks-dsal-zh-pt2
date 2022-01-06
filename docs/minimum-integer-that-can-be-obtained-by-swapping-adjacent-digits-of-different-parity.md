# 通过交换不同奇偶校验的相邻数字可以得到的最小整数

> 原文:[https://www . geesforgeks . org/通过交换不同奇偶校验的相邻数字可以获得的最小整数/](https://www.geeksforgeeks.org/minimum-integer-that-can-be-obtained-by-swapping-adjacent-digits-of-different-parity/)

给定一个整数 **N** ，任务是从给定的整数中找到可以得到的最小整数，使得不同奇偶校验的相邻数字可以交换任意次数。
两个不同奇偶性的数字意味着它们被二除时会有不同的余数。
**示例:**

> **输入:** N = 64432
> **输出:** 36442
> **说明:**
> 互换第 4 位和第 3 位数字；N = 64342
> 交换第三位和第二位数字；N = 63442
> 交换第二位和第一位数字；N = 36442
> **输入:**
> 3137
> **输出:**
> 3137

**方法:**方法的思路是用两个[栈](https://www.geeksforgeeks.org/stack-data-structure/)来保存数字的位数。

*   在一个堆栈中，可以存储可被二整除的数字。
*   在另一个堆栈中，可以存储不能被 2 整除的数字。
*   然后，元素按照与数字相反的顺序被推入两个堆栈。
*   现在，顶部包含较小元素的堆栈中的元素被弹出，并与答案连接，直到其中一个堆栈为空。
*   然后将堆栈的剩余元素与答案连接在一起，答案不为空，最后返回输出。

下面是上述方法的实现。

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ implementation of the above approach.
#include <bits/stdc++.h>
using namespace std;
// Function to return the minimum number
int minimumNo(int n)
{
    int ans = 0;
    stack<int> stack1;
    stack<int> stack2;
    while (n != 0) {
        int r = n % 10;

        // Store the elements which are
        // divisible by two in stack1
        if (r % 2 == 0) {
            stack1.push(r);
        }

        // Store the elements which are
        // not divisible by two in stack2.
        else {
            stack2.push(r);
        }
        n = n / 10;
    }

    while (!stack1.empty() && !stack2.empty()) {

        // Concatenate the answer with smaller value
        // of the topmost elements of both the
        // stacks and then pop that element
        if (stack1.top() < stack2.top()) {
            ans = ans * 10 + stack1.top();
            stack1.pop();
        }
        else {
            ans = ans * 10 + stack2.top();
            stack2.pop();
        }
    }

    // Concatenate the answer with remaining
    // values of stack1.
    while (!stack1.empty()) {
        ans = ans * 10 + stack1.top();
        stack1.pop();
    }

    // Concatenate the answer with remaining
    // values of stack2.
    while (!stack2.empty()) {
        ans = ans * 10 + stack2.top();
        stack2.pop();
    }
    return ans;
}

// Driver code
int main()
{
    int n1 = 64432;

    // Function calling
    cout << minimumNo(n1) << endl;

    int n2 = 3137;
    cout << minimumNo(n2) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach.
import java.util.*;

class GFG
{

// Function to return the minimum number
static int minimumNo(int n)
{
    int ans = 0;
    Stack<Integer> stack1 = new Stack<Integer>();
    Stack<Integer> stack2 = new Stack<Integer>();
    while (n != 0)
    {
        int r = n % 10;

        // Store the elements which are
        // divisible by two in stack1
        if (r % 2 == 0)
        {
            stack1.add(r);
        }

        // Store the elements which are
        // not divisible by two in stack2.
        else
        {
            stack2.add(r);
        }
        n = n / 10;
    }

    while (!stack1.isEmpty() && !stack2.isEmpty())
    {

        // Concatenate the answer with smaller value
        // of the topmost elements of both the
        // stacks and then pop that element
        if (stack1.peek() < stack2.peek())
        {
            ans = ans * 10 + stack1.peek();
            stack1.pop();
        }
        else
        {
            ans = ans * 10 + stack2.peek();
            stack2.pop();
        }
    }

    // Concatenate the answer with remaining
    // values of stack1.
    while (!stack1.isEmpty())
    {
        ans = ans * 10 + stack1.peek();
        stack1.pop();
    }

    // Concatenate the answer with remaining
    // values of stack2.
    while (!stack2.isEmpty())
    {
        ans = ans * 10 + stack2.peek();
        stack2.pop();
    }
    return ans;
}

// Driver code
public static void main(String[] args)
{
    int n1 = 64432;

    // Function calling
    System.out.print(minimumNo(n1) + "\n");

    int n2 = 3137;
    System.out.print(minimumNo(n2) + "\n");
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the above approach.

# Function to return the minimum number
def minimumNo(n):
    ans = 0
    stack1 = []
    stack2 = []
    while (n != 0):
        r = n % 10

        # Store the elements which are
        # divisible by two in stack1
        if (r % 2 == 0):
            stack1.append(r)

        # Store the elements which are
        # not divisible by two in stack2.
        else :
            stack2.append(r)

        n = n // 10
    while (len(stack1) > 0 and len(stack2) > 0):

        # Concatenate the answer with smaller value
        # of the topmost elements of both the
        # stacks and then pop that element
        if (stack1[-1] < stack2[-1]):
            ans = ans * 10 + stack1[-1]
            del stack1[-1]

        else:
            ans = ans * 10 + stack2[-1]
            del stack2[-1]

    # Concatenate the answer with remaining
    # values of stack1.
    while (len(stack1) > 0):
        ans = ans * 10 + stack1[-1]
        del stack1[-1]

    # Concatenate the answer with remaining
    # values of stack2.
    while (len(stack2) > 0):
        ans = ans * 10 + stack2[-1]
        del stack2[-1]

    return ans

# Driver code
n1 = 64432

# Function calling
print(minimumNo(n1))

n2 = 3137
print(minimumNo(n2))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the above approach.
using System;
using System.Collections.Generic;

class GFG
{

// Function to return the minimum number
static int minimumNo(int n)
{
    int ans = 0;
    Stack<int> stack1 = new Stack<int>();
    Stack<int> stack2 = new Stack<int>();
    while (n != 0)
    {
        int r = n % 10;

        // Store the elements which are
        // divisible by two in stack1
        if (r % 2 == 0)
        {
            stack1.Push(r);
        }

        // Store the elements which are
        // not divisible by two in stack2.
        else
        {
            stack2.Push(r);
        }
        n = n / 10;
    }

    while (stack1.Count != 0 && stack2.Count != 0)
    {

        // Concatenate the answer with smaller value
        // of the topmost elements of both the
        // stacks and then pop that element
        if (stack1.Peek() < stack2.Peek())
        {
            ans = ans * 10 + stack1.Peek();
            stack1.Pop();
        }
        else
        {
            ans = ans * 10 + stack2.Peek();
            stack2.Pop();
        }
    }

    // Concatenate the answer with remaining
    // values of stack1.
    while (stack1.Count != 0)
    {
        ans = ans * 10 + stack1.Peek();
        stack1.Pop();
    }

    // Concatenate the answer with remaining
    // values of stack2.
    while (stack2.Count != 0)
    {
        ans = ans * 10 + stack2.Peek();
        stack2.Pop();
    }
    return ans;
}

// Driver code
public static void Main(String[] args)
{
    int n1 = 64432;

    // Function calling
    Console.Write(minimumNo(n1) + "\n");

    int n2 = 3137;
    Console.Write(minimumNo(n2) + "\n");
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

      // JavaScript implementation
      // of the above approach.

      // Function to return the minimum number
      function minimumNo(n) {
        var ans = 0;
        var stack1 = [];
        var stack2 = [];
        while (n !== 0) {
          var r = n % 10;

          // Store the elements which are
          // divisible by two in stack1
          if (r % 2 === 0) {
            stack1.push(r);
          }

          // Store the elements which are
          // not divisible by two in stack2.
          else {
            stack2.push(r);
          }
          n = parseInt(n / 10);
        }

        while (stack1.length !== 0 && stack2.length !== 0)
        {
          // Concatenate the answer with smaller value
          // of the topmost elements of both the
          // stacks and then pop that element
          if (stack1[stack1.length - 1] <
          stack2[stack2.length - 1]) {
            ans = ans * 10 + stack1[stack1.length - 1];
            stack1.pop();
          } else {
            ans = ans * 10 + stack2[stack2.length - 1];
            stack2.pop();
          }
        }

        // Concatenate the answer with remaining
        // values of stack1.
        while (stack1.length !== 0) {
          ans = ans * 10 + stack1[stack1.length - 1];
          stack1.pop();
        }

        // Concatenate the answer with remaining
        // values of stack2.
        while (stack2.length !== 0) {
          ans = ans * 10 + stack2[stack2.length - 1];
          stack2.pop();
        }
        return ans;
      }

      // Driver code
      var n1 = 64432;

      // Function calling
      document.write(minimumNo(n1) + "<br>");

      var n2 = 3137;
      document.write(minimumNo(n2) + "<br>");

</script>
```

**Output:** 

```
36442
3137
```

**时间复杂度:**O(logN)
T3】辅助空间 : O(logN)。