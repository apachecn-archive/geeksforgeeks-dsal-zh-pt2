# 范围[0，N]内整数 K 的计数，使得(K 异或 K+1)等于(K+2 异或 K+3)

> 原文:[https://www . geesforgeks . org/整数计数-范围内的 k-0-n-这样-k-xor-k1-equals-k2-xor-k3/](https://www.geeksforgeeks.org/count-of-integers-k-in-range-0-n-such-that-k-xor-k1-equals-k2-xor-k3/)

给定一个整数 **N** ，任务是打印所有小于或等于 **N、**的非负整数 **K** 的计数，使得 **K** 和 **K+1** 的[逐位异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)等于 **K+2** 和 **K+3** 的[逐位异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)。

**示例:**

> **输入:** N = 3
> **输出:** 2
> **说明:**
> 满足条件的数字为:
> 
> 1.  K = 0，0 和 1 的按位异或等于 1，2 和 3 的按位异或也等于 1。
> 2.  K = 2，2 和 3 的按位异或等于 1，4 和 5 的按位异或也等于 1。
> 
> 因此，有 2 个数字满足条件。
> 
> **输入:**4
> T3】输出: 3

**天真法:**最简单的方法是[迭代范围](https://www.geeksforgeeks.org/loops-in-c-and-cpp/)**【0，N】**检查当前数字是否满足条件。如果满足，将计数增加 **1** 。核对所有数字后，打印计数值。

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)

**有效途径:**上述途径可以通过观察到范围**【0，N】**内的所有[偶数满足给定条件来优化。](https://www.geeksforgeeks.org/python-program-to-print-all-even-numbers-in-a-range/)

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count all the integers
// less than N satisfying the given
// condition
int countXor(int N)
{

    // Store the count of even
    // numbers less than N+1
    int cnt = N / 2 + 1;

    // Return the count
    return cnt;
}

// Driver Code
int main()
{
    // Given Input
    int N = 4;

    // Function Call
    cout << countXor(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program for the above approach
import java.io.*;

class GFG
{

    // Function to count all the integers
    // less than N satisfying the given
    // condition
    static int countXor(int N)
    {

        // Store the count of even
        // numbers less than N+1
        int cnt = (int) N / 2 + 1;

        // Return the count
        return cnt;
    }

    // Driver Code
    public static void main(String[] args)
    {

        // Given Input
        int N = 4;

        // Function Call
        System.out.println(countXor(N));

    }
}

// This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to count all the integers
# less than N satisfying the given
# condition
def countXor(N):

    # Store the count of even
    # numbers less than N+1
    cnt = N // 2 + 1

    # Return the count
    return cnt

# Driver Code
if __name__ == '__main__':

    # Given Input
    N = 4

    # Function Call
    print(countXor(N))

    # This code is contributed by SUTENDRA_GANGWAR.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to count all the integers
// less than N satisfying the given
// condition
static int countXor(int N)
{

    // Store the count of even
    // numbers less than N+1
    int cnt = (int)N / 2 + 1;

    // Return the count
    return cnt;
}

// Driver code
static void Main()
{

    // Given Input
    int N = 4;

    // Function Call
    Console.WriteLine(countXor(N));
}
}

// This code is contributed by abhinavjain194
```

## java 描述语言

```
<script>

        // JavaScript program for the above approach

        // Function to count all the integers
        // less than N satisfying the given
        // condition
        function countXor(N) {

            // Store the count of even
            // numbers less than N+1
            let cnt = Math.floor(N / 2) + 1;

            // Return the count
            return cnt;
        }

        // Driver Code

        // Given Input
        let N = 4;

        // Function Call
        document.write(countXor(N));

    // This code is contributed by Potta Lokesh

</script>
```

**Output**

```
3
```

***时间复杂度:**O(1)*
T5**辅助空间:** O(1)