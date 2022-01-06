# 求给定和为 N 的三元组(X，Y，Z)，两个数的 GCD 为第三个数

> 原文:[https://www . geesforgeks . org/find-a-triple-x-y-z-with-given-sum-as-n-and-gcd-of-two-numbers-is-third-number/](https://www.geeksforgeeks.org/find-a-triplet-x-y-z-with-given-sum-as-n-and-gcd-of-two-numbers-is-the-third-number/)

给定一个正整数 **N** ，任务是找到三个不同正整数(X，Y，Z)的三重，使得 X + Y + Z = N 和 X = [GCD](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/) (Y，Z)。

**示例:**

> **输入:** N = 12
> **输出:** 2 4 6
> 说明:三元组(2，4，6)是一组不同的整数，使得 2 + 4 + 6 = 12，2 = GCD(4，6)。
> 
> **输入:**N = 5675
> T3】输出: 1 2835 2839

**天真方法:**基本思想是用和 N 迭代[所有可能的(X，Y，Z)三元组，对于每个三元组，检查](https://www.geeksforgeeks.org/find-a-triplet-that-sum-to-a-given-value/) [GCD](https://www.geeksforgeeks.org/c-program-find-gcd-hcf-two-numbers/) (Y，Z) = X

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**有效方法:**上述方法可以进一步优化，观察到对于任何给定的 N，有以下三种情况:

*   情况 1:如果 **N** 为偶数，则有效的三元组为( **1** 、 **N/2** 、 **N/2 -1** )。
*   情况 2:如果 **N** 为奇数，( **N/2** )为偶数，则有效的三元组为( **1** 、 **N/2 + 1** 、 **N/2 -1** )。
*   情况 3:如果 **N** 为奇数并且( **N/2** )也为奇数，则有效的三元组为( **1** 、**N/2–2**、 **N/2 + 2** )。

因此，对于任何给定的 **N** ，识别案例并打印其各自的三联体。
以下是实施办法:

## C++

```
// C++ program of the above appraoch
#include <bits/stdc++.h>
using namespace std;

// Function to find a triplet (X, Y, Z)
// of distinct integers with their sum
// as N and GCD(Y, Z) = X
int printTriplet(int N)
{
    // Case 1 where N is even
    if (N % 2 == 0) {
        cout << 1 << " " << (N / 2)
<< " " << (N / 2) - 1;
    }
    else {

        // Case 2 where N is Odd
        // and N/2 is even
        if ((N / 2) % 2 == 0) {
            cout << 1 << " "
 << (N / 2) - 1 << " "
                 << (N / 2) + 1;
        }

        // Case 3 where N is Odd
        // and N/2 is also odd
        else {
            cout << 1 << " "
 << (N / 2) - 2 << " "
                 << (N / 2) + 2;
        }
    }
}

// Driver Code
int main()
{
    int N = 5875;
    printTriplet(N);

    return 0;
}
```

## 蟒蛇 3

```
# python3 program of the above appraoch

# Function to find a triplet (X, Y, Z)
# of distinct integers with their sum
# as N and GCD(Y, Z) = X
def printTriplet(N):

    # Case 1 where N is even
    if (N % 2 == 0):
        print(f"{1} {(N / 2)} {(N / 2) - 1}")

    else:

        # Case 2 where N is Odd
        # and N/2 is even
        if ((N // 2) % 2 == 0):
            print(f"{1} {(N // 2) - 1} {(N // 2) + 1}")

        # Case 3 where N is Odd
        # and N/2 is also odd
        else:
            print(f"{1} {(N // 2) - 2} {(N // 2) + 2}")

# Driver Code
if __name__ == "__main__":

    N = 5875
    printTriplet(N)

# This code is contributed by rakeshsahni
```

## C#

```
// C# program of the above appraoch
using System;

class GFG{

// Function to find a triplet (X, Y, Z)
// of distinct integers with their sum
// as N and GCD(Y, Z) = X
static void printTriplet(int N)
{

    // Case 1 where N is even
    if (N % 2 == 0)
    {
        Console.Write(1 + " " + (N / 2) + " " +
                               ((N / 2) - 1));
    }
    else
    {

        // Case 2 where N is Odd
        // and N/2 is even
        if ((N / 2) % 2 == 0)
        {
            Console.Write(1 + " " + ((N / 2) - 1) + " " +
                                    ((N / 2) + 1));
        }

        // Case 3 where N is Odd
        // and N/2 is also odd
        else
        {
            Console.Write(1 + " " + ((N / 2) - 2) + " " +
                                    ((N / 2) + 2));
        }
    }
}

// Driver Code
public static void Main()
{
    int N = 5875;

    printTriplet(N);
}
}

// This code is contributed by ukasp
```

## java 描述语言

```
<script>
       // JavaScript code for the above approach

       // Function to find a triplet (X, Y, Z)
       // of distinct integers with their sum
       // as N and GCD(Y, Z) = X
       function printTriplet(N)
       {

           // Case 1 where N is even
           if (N % 2 == 0) {
               document.write(1 + " " + Math.floor(N / 2)
                   + " " + (Math.floor(N / 2) - 1));
           }
           else {

               // Case 2 where N is Odd
               // and N/2 is even
               if ((N / 2) % 2 == 0) {
                   document.write(1 + " "
                       + (Math.floor(N / 2) - 1) + " "
                       + (Math.floor(N / 2) + 1));
               }

               // Case 3 where N is Odd
               // and N/2 is also odd
               else {
                   document.write(1 + " "
                       + (Math.floor(N / 2) - 2) + " "
                       + (Math.floor(N / 2) + 2));
               }
           }
       }

       // Driver Code
       let N = 5875;
       printTriplet(N);

 // This code is contributed by Potta Lokesh
   </script>
```

**Output**

```
1 2935 2939
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)