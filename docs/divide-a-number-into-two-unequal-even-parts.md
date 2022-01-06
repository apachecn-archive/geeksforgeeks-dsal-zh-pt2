# 将一个数分成两个不等的偶数部分

> 原文:[https://www . geesforgeks . org/将一个数分成两个不等的偶数部分/](https://www.geeksforgeeks.org/divide-a-number-into-two-unequal-even-parts/)

给定正整数 **N** 。任务是决定整数是否可以分成两个不等的正偶数部分。

**示例:**

> **输入:** N = 8
> **输出:** YES
> **说明:** 8 可以分为两个不同的偶数部分，即 2 和 6。
> 
> **输入:** N = 5
> **输出:** NO
> **说明:** 5 无论如何不能分成两个偶数部分。
> 
> **输入:** N = 4
> **输出:** NO
> **说明:** 4 可以分为 2 和 2 两个偶数部分。由于数字相等，输出为“否”

**先决条件:**了解 [if-else 条件语句](https://www.geeksforgeeks.org/decision-making-c-c-else-nested-else/)。

**方法:**问题的核心概念在于以下观察:

> 任何两个偶数的和总是偶数。相反，任何偶数都可以表示为两个偶数之和。

但是这里有两个例外

*   数字 2 在这里是个例外。只能表示为两个**奇数**数(1 + 1)的和。
*   数字 4 只能表示为**等于**的偶数(2 + 2)之和。

因此，只有当 **N 为偶数且不等于 2 或 4** 时，才有可能将 **N** 表示为两个偶数之和。如果 N 是奇数，就不可能把它分成两个偶数部分。遵循以下步骤:

1.  检查 N = 2 还是 N = 4。
2.  如果是，则打印否
3.  否则检查 N 是否为偶数(即 2 的倍数)
4.  如果是，则打印是。
5.  否则，打印否

下面是上述方法的实现。

## C++

```
// C++ code to implement above approach
#include<iostream>
using namespace std;

// Function to check if N can be divided 
// into two unequal even parts
bool evenParts(int N)
{   
    // Check if N is equal to 2 or 4  
    if(N == 2 || N == 4)
        return false;

    // Check if N is even
    if(N % 2 == 0)
        return true;
    else
        return false;
}

//Driver code
int main(){
   int N = 8;

   // Function call
   bool ans = evenParts(N);

   if(ans)
       std::cout << "YES" << '\n';
   else
       std::cout << "NO" << '\n';

   return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to implement above approach
import java.util.*;
public class GFG {

  // Function to check if N can be divided 
  // into two unequal even parts
  static boolean evenParts(int N)
  {   

    // Check if N is equal to 2 or 4  
    if(N == 2 || N == 4)
      return false;

    // Check if N is even
    if(N % 2 == 0)
      return true;
    else
      return false;
  }

  // Driver code
  public static void main(String args[])
  {
    int N = 8;

    // Function call
    boolean ans = evenParts(N);

    if(ans)
      System.out.println("YES");
    else
      System.out.println("NO");

  }
}

// This code is contributed by Samim Hossain Mondal.
```

## 蟒蛇 3

```
# Python code for the above approach

# Function to check if N can be divided
# into two unequal even parts
def evenParts(N):

    # Check if N is equal to 2 or 4
    if (N == 2 or N == 4):
        return False

    # Check if N is even
    if (N % 2 == 0):
        return True
    else:
        return False

# Driver code
N = 8

# Function call
ans = evenParts(N)
if (ans):
    print("YES")
else:
    print("NO")

# This code is contributed by Saurabh Jaiswal.
```

## C#

```
// C# code to implement above approach
using System;
class GFG {

  // Function to check if N can be divided 
  // into two unequal even parts
  static bool evenParts(int N)
  {   

    // Check if N is equal to 2 or 4  
    if(N == 2 || N == 4)
      return false;

    // Check if N is even
    if(N % 2 == 0)
      return true;
    else
      return false;
  }

  // Driver code
  public static void Main()
  {
    int N = 8;

    // Function call
    bool ans = evenParts(N);

    if(ans)
      Console.Write("YES" + '\n');
    else
      Console.Write("NO" + '\n');

  }
}

// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>
       // JavaScript code for the above approach

       // Function to check if N can be divided 
       // into two unequal even parts
       function evenParts(N)
       {

           // Check if N is equal to 2 or 4  
           if (N == 2 || N == 4)
               return false;

           // Check if N is even
           if (N % 2 == 0)
               return true;
           else
               return false;
       }

       // Driver code
       let N = 8;

       // Function call
       let ans = evenParts(N);
       if (ans)
           document.write("YES" + '<br>')
       else
           document.write("NO" + '<br>')

 // This code is contributed by Potta Lokesh
   </script>
```

**Output**

```
YES
```

**时间复杂度:**O(1)
T3】辅助空间: O(1)