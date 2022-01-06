# 将给定的数字分成两个偶数部分

> 原文:[https://www . geesforgeks . org/将给定数字分成两个偶数部分/](https://www.geeksforgeeks.org/divide-given-number-into-two-even-parts/)

给定一个数字 **N** ，任务是检查这个数字是否可以分成 2 个偶数部分。

**示例:**

> **输入:** N = 8
> **输出:** YES
> **说明:** 8 可以分为 2、6 或 4、4 两种偶数部分，因为两者都是偶数。
> 
> **输入:**N = 5
> T3】输出:否

**天真的方法:**检查直到 **N** 的所有数字对，这样它们都是偶数，并且它们都加到 **N** 上。如果可能，打印是，否则打印否

**时间复杂度:**O(N<sup>2</sup>)
T5】辅助空间: O(1)

**有效途径:**观察发现，除了 **2** 外，任何偶数都可以表示为两个偶数之和，没有两个偶数可以相加形成奇数。

下面是上述方法的实现。

## C++

```
// C++ code to implement above approach
#include <bits/stdc++.h>
using namespace std;

// Divide number into 2 even parts
bool divNum(int n)
{
    return (n <= 2
                ? false
                : (n % 2 == 0
                       ? true
                       : false));
}

// Driven Program
int main()
{
    int n = 8;
    cout << (divNum(n) ? "YES" : "NO")
         << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to implement above approach
import java.util.*;
public class GFG {

  // Divide number into 2 even parts
  static boolean divNum(int n)
  {
    return (n <= 2 ? false
            : (n % 2 == 0 ? true : false));
  }

  // Driven Program
  public static void main(String args[])
  {
    int n = 8;
    System.out.println(divNum(n) ? "YES" : "NO");
  }
}

// This code is contributed by Samim Hossain Mondal.
```

## 计算机编程语言

```
# Pyhton program for above approach

# Divide number into 2 even parts
def divNum(n):
    ans = False if n <= 2 else True if n % 2 == 0 else False                       
    return ans

# Driver Code
n = 8

if(divNum(n) == True):
    print("YES")
else:
    print("NO")

# This code is contributed by Samim Hossain Mondal.
```

## C#

```
// C# code to implement above approach
using System;
class GFG {

    // Divide number into 2 even parts
    static bool divNum(int n)
    {
        return (n <= 2 ? false
                       : (n % 2 == 0 ? true : false));
    }

    // Driven Program
    public static void Main()
    {
        int n = 8;
        Console.WriteLine(divNum(n) ? "YES" : "NO");
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
// Javascript code to implement above approach

// Divide number into 2 even parts
function divNum(n)
{
    return (n <= 2
                ? false
                : (n % 2 == 0
                       ? true
                       : false));
}

// Driven Program
let n = 8;
document.write((divNum(n) ? "YES" : "NO") + "\n");

// This code is contributed by Samim Hossin Mondal.
</script>
```

**Output**

```
YES
```

***时间复杂度:*** O(1)
***辅助空间:*** O(1)