# 范围【L，R】内可以表示为两个完美幂之和的数的计数

> 原文:[https://www . geeksforgeeks . org/范围内数字计数-l-r-可以表示为两个完美幂的和/](https://www.geeksforgeeks.org/count-of-numbers-in-range-l-r-which-can-be-represented-as-sum-of-two-perfect-powers/)

给定一个范围**【L，R】**，任务是找出范围**【L，R】**内的数字个数，这个范围可以是[表示为两个完美幂的和。](https://www.geeksforgeeks.org/check-if-a-number-can-be-expressed-as-sum-of-two-perfect-powers/)

**示例:**

> **输入:** L = 0，R = 1
> **输出:** 2
> **说明:**
> 有效数字为:
> 
> 1.  1 可以表示为，1 = 1 <sup>2</sup> + 0 <sup>2</sup> 。
> 2.  0 可以表示为，0 = 0 <sup>2</sup> + 0 <sup>2</sup> 。
> 
> 因此，此类数字的计数为 2。
> 
> **输入:** L = 5，R = 8
> **输出:** 2
> **说明:**
> 有效数字为:
> 
> 1.  5 可以表示为，5 = 1 <sup>2</sup> + 2 <sup>2</sup> 。
> 2.  8 可以表示为，0 = 0 <sup>2</sup> + 2 <sup>3</sup> 。
> 
> 因此，此类数字的计数为 2。

**方法:**给定的问题可以通过使用一些**数学观察**来解决。按照以下步骤解决问题:

*   从 **2** 生成所有小于 **R** 的数字的所有可能的幂，并将这些数字存储在一个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **幂【】**中。
*   初始化一个[布尔数组](https://www.geeksforgeeks.org/a-boolean-array-puzzle/)，把 **(R + 1)** 大小的 **arr[]** 设为 **0** 。
*   [生成数组中所有可能的不同对](https://www.geeksforgeeks.org/number-of-unique-pairs-in-an-array/) **幂[]** ，如果对的总和最多为**R**，则将其标记为数组中的**1****arr[]**。
*   现在，[求数组](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)**arr【】**的前缀和。
*   完成以上步骤后，打印**arr[R]–arr[L–1]**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the number of numbers
// that can be expressed in the form of
// the sum of two perfect powers
int TotalPerfectPowerSum(long long L,
                         long long R)
{
    // Stores all possible powers
    vector<long long> pows;

    // Push 1 and 0 in it
    pows.push_back(0);
    pows.push_back(1);

    // Iterate over all the exponents
    for (int p = 2; p < 25; p++) {

        // Iterate over all possible numbers
        long long int num = 2;

        // This loop will run for a
        // maximum of sqrt(R) times
        while ((long long int)(pow(num, p) + 0.5) <= R) {

            // Push this power in
            // the array pows[]
            pows.push_back(
                (long long int)(pow(num, p) + 0.5));

            // Increase the number
            num++;
        }
    }

    // Stores if i can be expressed as
    // the sum of perfect power or not
    int ok[R + 1];
    memset(ok, 0, sizeof(ok));

    // Iterate over all possible pairs
    // of the array pows[]
    for (int i = 0;
         i < pows.size(); i++) {

        for (int j = 0;
             j < pows.size(); j++) {

            if (pows[i] + pows[j] <= R
                and pows[i] + pows[j] >= L) {

                // The number is valid
                ok[pows[i] + pows[j]] = 1;
            }
        }
    }

    // Find the prefix sum of the
    // array ok[]
    for (int i = 0; i <= R; i++) {
        ok[i] += ok[i - 1];
    }

    // Return the count of required number
    return ok[R] - ok[L - 1];
}

// Driver Code
signed main()
{
    int L = 5, R = 8;
    cout << TotalPerfectPowerSum(L, R);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG {

    // Function to find the number of numbers
    // that can be expressed in the form of
    // the sum of two perfect powers
    static int TotalPerfectPowerSum(int L, int R)
    {
        // Stores all possible powers
        ArrayList<Integer> pows = new ArrayList<Integer>();

        // Push 1 and 0 in it
        pows.add(0);
        pows.add(1);

        // Iterate over all the exponents
        for (int p = 2; p < 25; p++) {

            // Iterate over all possible numbers
            int num = 2;

            // This loop will run for a
            // maximum of sqrt(R) times
            while ((int)(Math.pow(num, p) + 0.5) <= R) {

                // Push this power in
                // the array pows[]
                pows.add((int)(Math.pow(num, p) + 0.5));

                // Increase the number
                num++;
            }
        }

        // Stores if i can be expressed as
        // the sum of perfect power or not
        int[] ok = new int[R + 2];
        // memset(ok, 0, sizeof(ok));

        // Iterate over all possible pairs
        // of the array pows[]
        for (int i = 0; i < pows.size(); i++) {

            for (int j = 0; j < pows.size(); j++) {

                if (pows.get(i) + pows.get(j) <= R
                    && pows.get(i) + pows.get(j) >= L) {

                    // The number is valid
                    ok[pows.get(i) + pows.get(j)] = 1;
                }
            }
        }

        // Find the prefix sum of the
        // array ok[]
        for (int i = 1; i <= R; i++) {
            ok[i] += ok[i - 1];
        }

        // Return the count of required number
        return ok[R] - ok[L - 1];
    }

    // Driver Code
    public static void main(String args[])
    {

        int L = 5, R = 8;
        System.out.print(TotalPerfectPowerSum(L, R));
    }
}

// This code is contributed by avijitmondal1998.
```

## 蟒蛇 3

```
# python program for the above approach

# Function to find the number of numbers
# that can be expressed in the form of
# the sum of two perfect powers
def TotalPerfectPowerSum(L, R):

    # Stores all possible powers
    pows = []

    # Push 1 and 0 in it
    pows.append(0)
    pows.append(1)

    # Iterate over all the exponents
    for p in range(2, 25):

                # Iterate over all possible numbers
        num = 2

        # This loop will run for a
        # maximum of sqrt(R) times
        while ((int)(pow(num, p) + 0.5) <= R):

                        # Push this power in
                        # the array pows[]
            pows.append((int)(pow(num, p) + 0.5))

            # Increase the number
            num = num + 1

        # Stores if i can be expressed as
        # the sum of perfect power or not
    ok = [0 for _ in range(R + 1)]

    # int ok[R + 1];
    # memset(ok, 0, sizeof(ok));
    # Iterate over all possible pairs
    # of the array pows[]
    for i in range(0, int(len(pows))):
        for j in range(0, len(pows)):
            if (pows[i] + pows[j] <= R and pows[i] + pows[j] >= L):

                                # The number is valid
                ok[pows[i] + pows[j]] = 1

        # Find the prefix sum of the
        # array ok[]
    for i in range(0, R+1):
        ok[i] += ok[i - 1]

        # Return the count of required number
    return ok[R] - ok[L - 1]

# Driver Code
if __name__ == "__main__":
    L = 5
    R = 8
    print(TotalPerfectPowerSum(L, R))

    # This code is contributed by rakeshsahni
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG {

    // Function to find the number of numbers
    // that can be expressed in the form of
    // the sum of two perfect powers
    static int TotalPerfectPowerSum(long L, long R)
    {
        // Stores all possible powers
        List<long> pows = new List<long>();

        // Push 1 and 0 in it
        pows.Add(0);
        pows.Add(1);

        // Iterate over all the exponents
        for (int p = 2; p < 25; p++) {

            // Iterate over all possible numbers
            long num = 2;

            // This loop will run for a
            // maximum of sqrt(R) times
            while ((long)(Math.Pow(num, p) + 0.5) <= R) {

                // Push this power in
                // the array pows[]
                pows.Add((long)(Math.Pow(num, p) + 0.5));

                // Increase the number
                num++;
            }
        }

        // Stores if i can be expressed as
        // the sum of perfect power or not
        int[] ok = new int[R + 2];
        // memset(ok, 0, sizeof(ok));

        // Iterate over all possible pairs
        // of the array pows[]
        for (int i = 0; i < pows.Count; i++) {

            for (int j = 0; j < pows.Count; j++) {

                if (pows[i] + pows[j] <= R
                    && pows[i] + pows[j] >= L) {

                    // The number is valid
                    ok[pows[i] + pows[j]] = 1;
                }
            }
        }

        // Find the prefix sum of the
        // array ok[]
        for (int i = 1; i <= R; i++) {
            ok[i] += ok[i - 1];
        }

        // Return the count of required number
        return ok[R] - ok[L - 1];
    }

    // Driver Code
    public static void Main()
    {
        int L = 5, R = 8;
        Console.WriteLine(TotalPerfectPowerSum(L, R));
    }
}

// This code is contributed by ukasp.
```

## java 描述语言

```
<script>
       // JavaScript Program to implement
       // the above approach

       // Function to find the number of numbers
       // that can be expressed in the form of
       // the sum of two perfect powers
       function TotalPerfectPowerSum(L,
           R)
       {

           // Stores all possible powers
           let pows = [];

           // Push 1 and 0 in it
           pows.push(0);
           pows.push(1);

           // Iterate over all the exponents
           for (let p = 2; p < 25; p++) {

               // Iterate over all possible numbers
               let num = 2;

               // This loop will run for a
               // maximum of sqrt(R) times
               while (Math.floor(Math.pow(num, p) + 0.5) <= R) {

                   // Push this power in
                   // the array pows[]
                   pows.push(
                       Math.floor(Math.pow(num, p) + 0.5));

                   // Increase the number
                   num++;
               }
           }

           // Stores if i can be expressed as
           // the sum of perfect power or not

           let ok = new Array(R + 1).fill(0);

           // Iterate over all possible pairs
           // of the array pows[]
           for (let i = 0;
               i < pows.length; i++) {

               for (let j = 0;
                   j < pows.length; j++) {

                   if (pows[i] + pows[j] <= R
                       && pows[i] + pows[j] >= L) {

                       // The number is valid
                       ok[pows[i] + pows[j]] = 1;
                   }
               }
           }

           // Find the prefix sum of the
           // array ok[]
           for (let i = 1; i <= R; i++) {
               ok[i] += ok[i - 1];

           }

           // Return the count of required number
           return ok[R] - ok[L - 1];
       }

       // Driver Code
       let L = 5, R = 8;
       document.write(TotalPerfectPowerSum(L, R));

    // This code is contributed by Potta Lokesh
   </script>
```

**Output:** 

```
2
```

***时间复杂度:**O(R * log(R))*
T5**辅助空间:** O(R)