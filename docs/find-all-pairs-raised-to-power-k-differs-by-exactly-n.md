# 找出所有上升到 K 次方的对，正好相差 N

> 原文:[https://www . geeksforgeeks . org/find-all-pairs-raid-to-power-k-differents-by-just-n/](https://www.geeksforgeeks.org/find-all-pairs-raised-to-power-k-differs-by-exactly-n/)

给定两个正整数 **X** 和 **K** ，任务是找到所有可能的整数对 **(A，B)** ，使得整数对之间的差上升到幂 **K** 就是给定的整数 **X** 。如果没有这样的配对，则打印**-1”**。
***注:**的值 **K** 至少为**5**， **X** 最多为**10<sup>18</sup>**。*

**示例:**

> **输入:** X = 33，K = 5
> **输出:**
> (1，-2)
> (2，-1)
> **说明:**所有可能的对如下:
> 
> 1.  **(1，-2):** 的值(1<sup>5</sup>–(-2)<sup>5</sup>)= 33，等于 X(= 33)。
> 2.  **(2，-1):** 的值(2<sup>5</sup>–(-1)<sup>5</sup>)= 33，等于 X(= 33)。
> 
> 因此，总对数为 2。
> 
> **输入:** X = 10，K = 5
> T3】输出: 0

**逼近:**给定问题可以基于 **X** 的最大可能值可以是 **10 <sup>18</sup>** 的观察来求解。因此，整数对 **(A，B)** 的值将位于范围 **[-1000，1000]** 内。按照以下步骤解决问题:

*   初始化一个变量，比如说**将**计数为 **0** ，以计数满足给定条件的对的数量。
*   [在范围 **[-1000，1000]** 内生成所有可能的配对](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/) **(A，B)** ，如果**(A<sup>K</sup>–B<sup>K</sup>)**的值为 **X** ，则打印相应的配对，并按 **1** 递增**计数**。
*   完成上述步骤后，如果**计数**的值为 **0** ，则打印**-1”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to print pairs whose
// difference raised to the power K is X
void ValidPairs(int X, int K)
{
    // Stores the count of valid pairs
    long long int count = 0;

    // Iterate over the range [-1000, 1000]
    for (int A = -1000; A <= 1000; A++) {

        // Iterate over the range [-1000, 1000]
        for (int B = -1000; B <= 1000; B++) {

            // If the current pair satisfies
            // the given condition
            if (pow(A, K) - pow(B, K) == X) {

                // Increment the count by 1
                count++;
                cout << A << " " << B << endl;
            }
        }
    }

    // If no such pair exists
    if (count == 0) {
        cout << "-1";
    }
}

// Driver Code
int main()
{
    long long int X = 33;
    int K = 5;
    ValidPairs(X, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to print pairs whose
// difference raised to the power K is X
static void ValidPairs(int X, int K)
{

    // Stores the count of valid pairs
    int count = 0;

    // Iterate over the range [-1000, 1000]
    for(int A = -1000; A <= 1000; A++)
    {

        // Iterate over the range [-1000, 1000]
        for(int B = -1000; B <= 1000; B++)
        {

            // If the current pair satisfies
            // the given condition
            if (Math.pow(A, K) - Math.pow(B, K) == X)
            {

                // Increment the count by 1
                count++;
                System.out.println(A + " " + B );
            }
        }
    }

    // If no such pair exists
    if (count == 0)
    {
        System.out.println("-1");
    }
}

// Driver Code
public static void main(String args[])
{
    int X = 33;
    int K = 5;

    ValidPairs(X, K);
}
}

// This code is contributed by souravghosh0416
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to prpairs whose
# difference raised to the power K is X
def ValidPairs(X, K) :

    # Stores the count of valid pairs
    count = 0

    # Iterate over the range [-1000, 1000]
    for A in range(-1000, 1001, 1):

        # Iterate over the range [-1000, 1000]
        for B in range(-1000, 1001, 1):

            # If the current pair satisfies
            # the given condition
            if (pow(A, K) - pow(B, K) == X) :

                # Increment the count by 1
                count += 1
                print(A, B)

    # If no such pair exists
    if (count == 0) :
        cout << "-1"

# Driver Code
X = 33
K = 5
ValidPairs(X, K)

# This code is contributed by sanjoy_62.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to print pairs whose
// difference raised to the power K is X
static void ValidPairs(int X, int K)
{

    // Stores the count of valid pairs
    int count = 0;

    // Iterate over the range [-1000, 1000]
    for(int A = -1000; A <= 1000; A++)
    {

        // Iterate over the range [-1000, 1000]
        for(int B = -1000; B <= 1000; B++)
        {

            // If the current pair satisfies
            // the given condition
            if (Math.Pow(A, K) - Math.Pow(B, K) == X)
            {

                // Increment the count by 1
                count++;
                Console.WriteLine(A + " " + B);
            }
        }
    }

    // If no such pair exists
    if (count == 0)
    {
        Console.WriteLine("-1");
    }
}

// Driver Code
static public void Main()
{
    int X = 33;
    int K = 5;

    ValidPairs(X, K);
}
}

// This code is contributed by Dharanendra L V.
```

## java 描述语言

```
<script>
// javascript program for the above approach

    // Function to prvar pairs whose
    // difference raised to the power K is X
    function ValidPairs(X , K) {

        // Stores the count of valid pairs
        var count = 0;

        // Iterate over the range [-1000, 1000]
        for (A = -1000; A <= 1000; A++) {

            // Iterate over the range [-1000, 1000]
            for (B = -1000; B <= 1000; B++) {

                // If the current pair satisfies
                // the given condition
                if (Math.pow(A, K) - Math.pow(B, K) == X) {

                    // Increment the count by 1
                    count++;
                    document.write(A + " " + B +"<br/>");
                }
            }
        }

        // If no such pair exists
        if (count == 0) {
            document.write("-1<br/>");
        }
    }

    // Driver Code
        var X = 33;
        var K = 5;
        ValidPairs(X, K);

// This code is contributed by gauravrajput1
</script>
```

**Output:** 

```
1 -2
2 -1
```

***时间复杂度:**O(2000 * 2000)*
T5**辅助空间:** O(1)