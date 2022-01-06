# 每 K 个连续数字之和相等的 N 位数计数

> 原文:[https://www . geeksforgeeks . org/n 位数计数-其每 k 个连续位数的总和等于/](https://www.geeksforgeeks.org/count-of-n-digit-numbers-whose-sum-of-every-k-consecutive-digits-is-equal/)

给定两个整数 **N** 和 **K** ，任务是找出 **N** 位数的总数，使得该数的每一个 **K** 连续位数的和相等。

**示例:**

> **输入:** N = 2，K = 1
> **输出:** 9
> **说明:**
> 数字为 11、22、33、44、55、66、77、88、99，每 1 个连续数字的和分别等于 1、2、3、4、5、6、7、8、9。
> 
> **输入:** N = 3，K = 2
> T3】输出: 90

**天真方法:**迭代所有可能的 **N 位**数字，并计算该数字的每个 **K** 连续数字的总和。如果所有的总和相等，那么包括这是计数否则检查下一个数字。

下面是上述方法的实现:

## C++

```
// C++ program for
// the above approach

#include<bits/stdc++.h>
using namespace std;

// Function to count the number of
// N-digit numbers such that sum of
// every k consecutive digits are equal
int countDigitSum(int N, int K)
{

    // Range of numbers
    int l = (int)pow(10, N - 1),
        r = (int)pow(10, N) - 1;
    int count = 0;

    for(int i = l; i <= r; i++)
    {
        int num = i;

        // Extract digits of the number
        int digits[N];

        for(int j = N - 1; j >= 0; j--)
        {
            digits[j] = num % 10;
            num /= 10;
        }
        int sum = 0, flag = 0;

        // Store the sum of first K digits
        for(int j = 0; j < K; j++)
            sum += digits[j];

        // Check for every
        // k-consecutive digits
        for(int j = 1; j < N - K + 1; j++)
        {
            int curr_sum = 0;

            for(int m = j; m < j + K; m++)
                    curr_sum += digits[m];

            // If sum is not equal
            // then break the loop
            if (sum != curr_sum)
            {
                flag = 1;
                break;
            }
        }

        // Increment the count if it
        // satisfy the given condition
        if (flag == 0)
        {
            count++;
        }
    }
    return count;
}

// Driver Code
int main()
{

    // Given N and K
    int N = 2, K = 1;

    // Function call
    cout << countDigitSum(N, K);
    return 0;
}

// This code is contributed by target_2.
```

## C

```
// C program for the above approach
#include <math.h>
#include <stdio.h>

// Function to count the number of
// N-digit numbers such that sum of
// every k consecutive digits are equal
int countDigitSum(int N, int K)
{

    // Range of numbers
    int l = (int)pow(10, N - 1),
        r = (int)pow(10, N) - 1;
    int count = 0;

    for(int i = l; i <= r; i++)
    {
        int num = i;

        // Extract digits of the number
        int digits[N];

        for(int j = N - 1; j >= 0; j--)
        {
            digits[j] = num % 10;
            num /= 10;
        }
        int sum = 0, flag = 0;

        // Store the sum of first K digits
        for(int j = 0; j < K; j++)
            sum += digits[j];

        // Check for every
        // k-consecutive digits
        for(int j = 1; j < N - K + 1; j++)
        {
            int curr_sum = 0;

            for(int m = j; m < j + K; m++)
                    curr_sum += digits[m];

            // If sum is not equal
            // then break the loop
            if (sum != curr_sum)
            {
                flag = 1;
                break;
            }
        }

        // Increment the count if it
        // satisfy the given condition
        if (flag == 0)
        {
            count++;
        }
    }
    return count;
}

// Driver code
int main()
{

    // Given N and K
    int N = 2, K = 1;

    // Function call
    printf("%d", countDigitSum(N, K));

    return 0;
}

// This code is contributed by piyush3010
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

class GFG {

    // Function to count the number of
    // N-digit numbers such that sum of
    // every k consecutive digits are equal
    static int countDigitSum(int N, int K)
    {
        // Range of numbers
        int l = (int)Math.pow(10, N - 1),
            r = (int)Math.pow(10, N) - 1;
        int count = 0;

        for (int i = l; i <= r; i++) {
            int num = i;

            // Extract digits of
            // the number
            int digits[] = new int[N];

            for (int j = N - 1;
                 j >= 0; j--) {

                digits[j] = num % 10;
                num /= 10;
            }
            int sum = 0, flag = 0;

            // Store the sum of
            // first K digits
            for (int j = 0; j < K; j++)
                sum += digits[j];

            // Check for every
            // k-consecutive digits
            for (int j = 1;
                 j < N - K + 1; j++) {

                int curr_sum = 0;

                for (int m = j;
                     m < j + K; m++) {

                    curr_sum += digits[m];
                }

                // If sum is not equal
                // then break the loop
                if (sum != curr_sum) {
                    flag = 1;
                    break;
                }
            }

            // Increment the count if it
            // satisfy the given condition
            if (flag == 0) {
                count++;
            }
        }

        return count;
    }

    // Driver Code
    public static void
        main(String[] args)
    {
        // Given N and K
        int N = 2, K = 1;

        // Function call
        System.out.print(countDigitSum(N, K));
    }
}
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count the number of
# N-digit numbers such that sum of
# every k consecutive digits are equal
def countDigitSum(N, K):

    # Range of numbers
    l = pow(10, N - 1)
    r = pow(10, N) - 1
    count = 0

    for i in range(l, r + 1):
        num = i

        # Extract digits of the number
        digits = [0] * N

        for j in range(N - 1, -1, -1):
            digits[j] = num % 10
            num //= 10

        sum = 0
        flag = 0

        # Store the sum of first K digits
        for j in range(0, K):
            sum += digits[j]

        # Check for every
        # k-consecutive digits
        for j in range(1, N - K + 1):
            curr_sum = 0

            for m in range(j, j + K):
                    curr_sum += digits[m]

            # If sum is not equal
            # then break the loop
            if (sum != curr_sum):
                flag = 1
                break

        # Increment the count if it
        # satisfy the given condition
        if (flag == 0):
            count += 1

    return count

# Driver code

# Given N and K
N = 2
K = 1

# Function call
print(countDigitSum(N, K))

# This code is contributed by sanjoy_62
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to count the number of
// N-digit numbers such that sum of
// every k consecutive digits are equal
static int countDigitSum(int N, int K)
{

    // Range of numbers
    int l = (int)Math.Pow(10, N - 1),
        r = (int)Math.Pow(10, N) - 1;

    int count = 0;

    for(int i = l; i <= r; i++)
    {
        int num = i;

        // Extract digits of
        // the number
        int[] digits = new int[N];

        for(int j = N - 1; j >= 0; j--)
        {
            digits[j] = num % 10;
            num /= 10;
        }
        int sum = 0, flag = 0;

        // Store the sum of
        // first K digits
        for(int j = 0; j < K; j++)
            sum += digits[j];

        // Check for every
        // k-consecutive digits
        for(int j = 1; j < N - K + 1; j++)
        {
            int curr_sum = 0;

            for(int m = j; m < j + K; m++)
            {
                curr_sum += digits[m];
            }

            // If sum is not equal
            // then break the loop
            if (sum != curr_sum)
            {
                flag = 1;
                break;
            }
        }

        // Increment the count if it
        // satisfy the given condition
        if (flag == 0)
        {
            count++;
        }
    }
    return count;
}

// Driver Code
public static void Main()
{

    // Given N and K
    int N = 2, K = 1;

    // Function call
    Console.Write(countDigitSum(N, K));
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to count the number of
// N-digit numbers such that sum of
// every k consecutive digits are equal
function countDigitSum(N, K)
{

    // Range of numbers
    let l = parseInt(Math.pow(10, N - 1)),
        r = parseInt(Math.pow(10, N) - 1);
    let count = 0;

    for(let i = l; i <= r; i++)
    {
        let num = i;

        // Extract digits of the number
        let digits = new Array(N);

        for(let j = N - 1; j >= 0; j--)
        {
            digits[j] = num % 10;
            num = parseInt(num/10);
        }
        let sum = 0, flag = 0;

        // Store the sum of first K digits
        for(let j = 0; j < K; j++)
            sum += digits[j];

        // Check for every
        // k-consecutive digits
        for(let j = 1; j < N - K + 1; j++)
        {
            let curr_sum = 0;

            for(let m = j; m < j + K; m++)
                    curr_sum += digits[m];

            // If sum is not equal
            // then break the loop
            if (sum != curr_sum)
            {
                flag = 1;
                break;
            }
        }

        // Increment the count if it
        // satisfy the given condition
        if (flag == 0)
        {
            count++;
        }
    }
    return count;
}

// Driver code

    // Given N and K
    let N = 2, K = 1;

    // Function call
    document.write(countDigitSum(N, K));

// This code is contributed by souravmahato348.

</script>
```

**Output:** 

```
9
```

**时间复杂度:**O(10<sup>N</sup>* N * K)
T5】辅助空间: O(N)

**高效方法:**优化上述天真方法的思路是使用[滑动窗口技术](https://www.geeksforgeeks.org/window-sliding-technique/)检查数字的 K 个连续数字的和是否相等。以下是步骤:

1.  获取数字的范围，即 **10 <sup>N-1</sup> 到 10<sup>N</sup>T5。**
2.  对于上述范围内的每个数字，考虑一个长度为 **K** 和[的窗口，求每个数字的和](https://www.geeksforgeeks.org/program-for-sum-of-the-digits-of-a-given-number/)。将此金额存储为 **S** 。
3.  通过在总和中包含下一个 **K** 位，使用滑动窗口找到下一个 K 位的总和，并从总和中移除前一个 **K** 位。
4.  如果得到的和等于上面的和 **S** 然后检查下一个 **K** 数字。
5.  否则，对下一个数字重复上述步骤。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count the number of
// N-digit numbers such that sum of
// every k consecutive digits are equal
int countDigitSum(int N, int K)
{

    // Range of numbers
    int l = (int)pow(10, N - 1),
        r = (int)pow(10, N) - 1;

    int count = 0;
    for(int i = l; i <= r; i++)
    {
        int num = i;

        // Extract digits of the number
        int digits[N];
        for (int j = N - 1; j >= 0; j--)
        {
            digits[j] = num % 10;
            num /= 10;
        }
        int sum = 0, flag = 0;

        // Store the sum of first K digits
        for(int j = 0; j < K; j++)
            sum += digits[j];

        // Check for every
        // k-consecutive digits
        // using sliding window
        for(int j = K; j < N; j++)
        {
            if(sum - digits[j - K] +
                     digits[j] != sum)
            {
                flag = 1;
                break;
            }
        }
        if (flag == 0)
            count++;
    }
    return count;
}

// Driver Code
int main()
{

    // Given integer N and K
    int N = 2, K = 1;

    cout<< countDigitSum(N, K)<<endl;

    return 0;
}

// This code is contributed by itsok.
```

## C

```
// C program for the above approach
#include <stdio.h>
#include <math.h>

// Function to count the number of
// N-digit numbers such that sum of
// every k consecutive digits are equal
int countDigitSum(int N, int K)
{

    // Range of numbers
    int l = (int)pow(10, N - 1),
        r = (int)pow(10, N) - 1;

    int count = 0;
    for(int i = l; i <= r; i++)
    {
        int num = i;

        // Extract digits of the number
        int digits[N];
        for (int j = N - 1; j >= 0; j--)
        {
            digits[j] = num % 10;
            num /= 10;
        }
        int sum = 0, flag = 0;

        // Store the sum of first K digits
        for(int j = 0; j < K; j++)
            sum += digits[j];

        // Check for every
        // k-consecutive digits
        // using sliding window
        for(int j = K; j < N; j++)
        {
            if(sum - digits[j - K] +
                     digits[j] != sum)
            {
                flag = 1;
                break;
            }
        }
        if (flag == 0)
            count++;
    }
    return count;
}

// Driver Code
int main()
{

    // Given integer N and K
    int N = 2, K = 1;

    printf("%d", countDigitSum(N, K));

    return 0;
}

// This code is contributed by piyush3010
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG {

    // Function to count the number of
    // N-digit numbers such that sum of
    // every k consecutive digits are equal
    static int countDigitSum(int N, int K)
    {
        // Range of numbers
        int l = (int)Math.pow(10, N - 1),
            r = (int)Math.pow(10, N) - 1;
        int count = 0;
        for (int i = l; i <= r; i++) {
            int num = i;

            // Extract digits of the number
            int digits[] = new int[N];
            for (int j = N - 1; j >= 0; j--) {
                digits[j] = num % 10;
                num /= 10;
            }
            int sum = 0, flag = 0;

            // Store the sum of
            // first K digits
            for (int j = 0; j < K; j++)
                sum += digits[j];

            // Check for every
            // k-consecutive digits
            // using sliding window
            for (int j = K; j < N; j++) {

                if (sum - digits[j - K]
                        + digits[j]
                    != sum) {
                    flag = 1;
                    break;
                }
            }
            if (flag == 0) {
                count++;
            }
        }
        return count;
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given integer N and K
        int N = 2, K = 1;
        System.out.print(countDigitSum(N, K));
    }
}

/* This code is contributed by piyush3010 */
```

## 蟒蛇 3

```
# Python3 program for the
# above approach

# Function to count the
# number of N-digit numbers
# such that sum of every k
# consecutive digits are equal
def countDigitSum(N, K):

    # Range of numbers
    l = pow(10, N - 1);
    r = pow(10, N) - 1;
    count = 0;

    for i in range(1, r + 1):
        num = i;

        # Extract digits of
        # the number
        digits = [0] * (N);

        for j in range(N - 1,
                       0, -1):
            digits[j] = num % 10;
            num //= 10;

        sum = 0;
        flag = 0;

        # Store the sum of
        # first K digits
        for j in range(0, K):
            sum += digits[j];

        # Check for every
        # k-consecutive digits
        # using sliding window
        for j in range(K, N):
            if (sum - digits[j - K] +
                digits[j] != sum):
                flag = 1;
                break;

        if (flag == 0):
            count += 1;

    return count;

# Driver Code
if __name__ == '__main__':

    # Given integer N and K
    N = 2;
    K = 1;
    print(countDigitSum(N, K));

# This code is contributed by shikhasingrajput
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to count the number of
// N-digit numbers such that sum of
// every k consecutive digits are equal
static int countDigitSum(int N, int K)
{

    // Range of numbers
    int l = (int)Math.Pow(10, N - 1),
        r = (int)Math.Pow(10, N) - 1;
    int count = 0;

    for(int i = l; i <= r; i++)
    {
        int num = i;

        // Extract digits of the number
        int[] digits = new int[N];
        for(int j = N - 1; j >= 0; j--)
        {
            digits[j] = num % 10;
            num /= 10;
        }
        int sum = 0, flag = 0;

        // Store the sum of
        // first K digits
        for(int j = 0; j < K; j++)
            sum += digits[j];

        // Check for every
        // k-consecutive digits
        // using sliding window
        for(int j = K; j < N; j++)
        {
            if (sum - digits[j - K] +
                      digits[j] != sum)
            {
                flag = 1;
                break;
            }
        }
        if (flag == 0)
        {
            count++;
        }
    }
    return count;
}

// Driver Code
public static void Main()
{

    // Given N and K
    int N = 2, K = 1;

    // Function call
    Console.Write(countDigitSum(N, K));
}
}

// This code is contributed by sanjoy_62
```

## java 描述语言

```
<script>

// Javascript program for the above approach

    // Function to count the number of
    // N-digit numbers such that sum of
    // every k consecutive digits are equal
    function countDigitSum(N , K)
    {
        // Range of numbers
        var l = parseInt( Math.pow(10, N - 1)),
        var r = parseInt( Math.pow(10, N) - 1);
        var count = 0;
        for (i = l; i <= r; i++) {
            var num = i;

            // Extract digits of the number
            var digits = Array(N).fill(0);
            for (j = N - 1; j >= 0; j--) {
                digits[j] = num % 10;
                num = parseInt(num/10);
            }
            var sum = 0, flag = 0;

            // Store the sum of
            // first K digits
            for (j = 0; j < K; j++)
                sum += digits[j];

            // Check for every
            // k-consecutive digits
            // using sliding window
            for (j = K; j < N; j++) {

                if (sum - digits[j - K] + digits[j] != sum) {
                    flag = 1;
                    break;
                }
            }
            if (flag == 0) {
                count++;
            }
        }
        return count;
    }

    // Driver Code

        // Given integer N and K
        var N = 2, K = 1;
        document.write(countDigitSum(N, K));

// This code contributed by umadevi9616

</script>
```

**Output:** 

```
9
```

**时间复杂度:***O(10<sup>N</sup>* N)*
**辅助空间:** *O(N)*