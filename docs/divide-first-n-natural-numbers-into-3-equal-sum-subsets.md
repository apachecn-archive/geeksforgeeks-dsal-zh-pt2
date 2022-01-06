# 将前 N 个自然数分成 3 个等和子集

> 原文:[https://www . geesforgeks . org/将第一个 n 个自然数分成 3 个等和子集/](https://www.geeksforgeeks.org/divide-first-n-natural-numbers-into-3-equal-sum-subsets/)

给定一个整数 **N** ，任务是检查来自范围**【1，N】**的元素是否可以分成三个非空的等和子集。如果可能，则打印**是**否则打印**否**。

**示例:**

> **输入:** N = 5
> **输出:**是
> 可能的子集有{1，4}、{2，3}和{5}。
> (1 + 4) = (2 + 3) = (5)
> 
> **输入:**N = 3
> T3】输出:否

**进场:**有两种情况:

1.  **如果 N ≤ 3:** 在这种情况下，不可能在满足给定条件的子集中划分元素。所以，打印**号**。
2.  **如果 N > 3:** 在这种情况下，只有当范围**【1，N】**的所有元素之和可被 **3** 整除时才有可能，这很容易计算为**之和= (N * (N + 1)) / 2** 。现在，如果**总和% 3 = 0** 则打印**是**否则打印**否**。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <iostream>
using namespace std;

// Function that returns true
// if the subsets are possible
bool possible(int n)
{

    // If n <= 3 then it is not possible
    // to divide the elements in three subsets
    // satisfying the given conditions
    if (n > 3) {

        // Sum of all the elements
        // in the range [1, n]
        int sum = (n * (n + 1)) / 2;

        // If the sum is divisible by 3
        // then it is possible
        if (sum % 3 == 0) {
            return true;
        }
    }
    return false;
}

// Driver code
int main()
{
    int n = 5;

    if (possible(n))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.math.*;

class GFG
{

    // Function that returns true
    // if the subsets are possible
    public static boolean possible(int n)
    {

        // If n <= 3 then it is not possible
        // to divide the elements in three subsets
        // satisfying the given conditions
        if (n > 3)
        {

            // Sum of all the elements
            // in the range [1, n]
            int sum = (n * (n + 1)) / 2;

            // If the sum is divisible by 3
            // then it is possible
            if (sum % 3 == 0)
            {
                return true;
            }
        }
        return false;
    }

    // Driver code
    public static void main(String[] args)
    {
        int n = 5;

        if (possible(n))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}

// This code is contributed by Naman_Garg
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function that returns true
# if the subsets are possible
def possible(n) :

    # If n <= 3 then it is not possible
    # to divide the elements in three subsets
    # satisfying the given conditions
    if (n > 3) :

        # Sum of all the elements
        # in the range [1, n]
        sum = (n * (n + 1)) // 2;

        # If the sum is divisible by 3
        # then it is possible
        if (sum % 3 == 0) :
            return True;

    return False;

# Driver code
if __name__ == "__main__" :

    n = 5;

    if (possible(n)) :
        print("Yes");
    else :
        print("No");

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function that returns true
// if the subsets are possible
public static bool possible(int n)
{

    // If n <= 3 then it is not possible
    // to divide the elements in three subsets
    // satisfying the given conditions
    if (n > 3)
    {

        // Sum of all the elements
        // in the range [1, n]
        int sum = (n * (n + 1)) / 2;

        // If the sum is divisible by 3
        // then it is possible
        if (sum % 3 == 0)
        {
            return true;
        }
    }
    return false;
}

// Driver code
static public void Main ()
{
    int n = 5;

    if (possible(n))
        Console.Write("Yes");
    else
        Console.Write("No");
}
}

// This code is contributed by ajit
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function that returns true
// if the subsets are possible
function possible(n)
{

    // If n <= 3 then it is not possible
    // to divide the elements in three subsets
    // satisfying the given conditions
    if (n > 3)
    {

        // Sum of all the elements
        // in the range [1, n]
        let sum = parseInt((n * (n + 1)) / 2);

        // If the sum is divisible by 3
        // then it is possible
        if (sum % 3 == 0)
        {
            return true;
        }
    }
    return false;
}

// Driver code
let n = 5;

if (possible(n))
    document.write("Yes");
else
    document.write("No");

// This code is contributed by rishavmahato348

</script>
```

**Output:** 

```
Yes
```