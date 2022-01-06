# 获得 N

所需的价值等于 2 的幂的硬币的最小数量

> 原文:[https://www . geeksforgeeks . org/最低硬币数量-价值等于 2 的幂-需要获得-n/](https://www.geeksforgeeks.org/minimum-number-of-coins-having-value-equal-to-powers-of-2-required-to-obtain-n/)

给定一个整数 **N** ，任务是找到兑换 **N** 美分所需的最小硬币数量形式**2<sup>I</sup>T5。**

**示例:**

> **输入:** N = 5
> **输出:** 2
> **说明:**
> 硬币可能的取值为:{1，2，4，8，…}
> 为 N 美分进行兑换的可能方式如下:
> 5 = 1+1+1+1+1+1
> 5 = 1+2+2
> 5 = 1+4(最小值)
> 因此，需要的输出为 2
> 
> **输入:**N = 4
> T3】输出: 4

**天真方法:**解决这个问题最简单的方法是将硬币的所有可能值存储在一个数组中，并使用动态编程打印出兑换 N 美分所需的[最小硬币数。
***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*](https://www.geeksforgeeks.org/find-minimum-number-of-coins-that-make-a-change/)

**高效方法:**上述方法可以利用任何数字都可以用 **2** s 的幂的形式表示这一事实进行优化，其思想是[对 **N**](https://www.geeksforgeeks.org/count-set-bits-in-an-integer/) 的设定位进行计数，并打印得到的计数。按照以下步骤解决问题:

*   迭代 **N** 二进制表示中的位，检查当前位是否置位。如果发现为真，则增加计数。
*   最后，打印获得的总计数。

下面是上述方法的实现:

## C++

```
// C++ program for above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count of set bit in N
void count_setbit(int N)
{

    // Stores count of set bit in N
    int result = 0;

    // Iterate over the range [0, 31]
    for (int i = 0; i < 32; i++) {

        // If current bit is set
        if ((1 << i) & N) {

            // Update result
            result++;
        }
    }
    cout << result << endl;
}

// Driver Code
int main()
{
    int N = 43;

    count_setbit(N);
    return 0;
}
```

## C

```
// C program for above approach
#include <stdio.h>

// Function to count of set bit in N
void count_setbit(int N)
{

    // Stores count of set bit in N
    int result = 0;

    // Iterate over the range [0, 31]
    for (int i = 0; i < 32; i++) {

        // If current bit is set
        if ((1 << i) & N) {

            // Update result
            result++;
        }
    }
    printf("%d\n", result);
}

// Driver Code
int main()
{
    int N = 43;

    count_setbit(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach
public class Main {

    // Function to count of set bit in N
    public static void count_setbit(int N)
    {
        // Stores count of set bit in N
        int result = 0;

        // Iterate over the range [0, 31]
        for (int i = 0; i < 32; i++) {

            // If current bit is set
            if (((1 << i) & N) > 0) {

                // Update result
                result++;
            }
        }

        System.out.println(result);
    }

    // Driver Code
    public static void main(String[] args)
    {

        int N = 43;
        count_setbit(N);
    }
}
```

## 计算机编程语言

```
# Python program for above approach

# Function to count of set bit in N
def count_setbit(N):

    # Stores count of set bit in N
    result = 0

    # Iterate over the range [0, 31]
    for i in range(32):

       # If current bit is set  
       if( (1 << i) & N ):

           # Update result
           result = result + 1

    print(result)

if __name__ == '__main__':

    N = 43
    count_setbit(N)
```

## C#

```
// C# program for above approach
using System;
class GFG {

    // Function to count of setbit in N
    static void count_setbit(int N)
    {

        // Stores count of setbit in N
        int result = 0;

        // Iterate over the range [0, 31]
        for (int i = 0; i < 32; i++) {

            // If current bit is set
            if (((1 << i) & N) > 0) {

                // Update result
                result++;
            }
        }

        Console.WriteLine(result);
    }

    // Driver Code
    static void Main()
    {

        int N = 43;
        count_setbit(N);
    }
}
```

## java 描述语言

```
<script>
// Javascript program to implement
// the above approach

    // Function to count of set bit in N
    function count_setbit(N)
    {
        // Stores count of set bit in N
        let result = 0;

        // Iterate over the range [0, 31]
        for (let i = 0; i < 32; i++) {

            // If current bit is set
            if (((1 << i) & N) > 0) {

                // Update result
                result++;
            }
        }
        document.write(result);
    }

// Driver Code
        let N = 43;
        count_setbit(N); 

    // This code is contributed by souravghosh0416.
</script>
```

**Output:** 

```
4
```

***时间复杂度:**O(log<sub>2</sub>(N))*
***辅助空间:** O(1)*