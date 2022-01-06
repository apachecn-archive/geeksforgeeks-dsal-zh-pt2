# 最小化 N，使得所有因子的计数之和直到 N 大于或等于 X

> 原文:[https://www . geesforgeks . org/minimum-n-这样所有因子的计数总和-up-n-大于或等于-x/](https://www.geeksforgeeks.org/minimise-n-such-that-sum-of-count-of-all-factors-upto-n-is-greater-than-or-equal-to-x/)

给定一个数 **X** ，任务是找到最小数 **N** ，使得从 **1 到 N** 的所有因子的计数之和大于等于 **X** 。
**示例:**

> **输入:** X = 10
> **输出:** 5
> **解释:**
> 总因子 1 = 1 (1)
> 总因子 2 = 2 (1，2)
> 总因子 3 = 2 (1，3)
> 总因子 4 = 3 (1，2，4)
> 总因子 5 = 2 (1， 5)
> 总计数= 1 + 2 + 2 + 3 + 2 = 10 大于等于 X 即 10
> **输入:** X = 19
> **输出:** 8
> **解释:**
> 总因子 1 = 1 (1)
> 总因子 2 = 2 (1，2)
> 总因子 3 = 2 (1，3)
> 总 4)
> 总因子 5 = 2 (1，5)
> 总因子 6 = 2 (1，2，3，6)
> 总因子 7 = 2 (1，7)
> 总因子 8 = 2 (1，2，4，8)
> 总计数= 1 + 2 + 2 + 3 + 2 + 4 + 2 + 4 = 20 大于等于 X 即 19

**天真法:**天真法是从 **1** 开始运行一个循环，直到因子总数大于等于 **X** 。
以下是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

#define MAX 1000050
#define lli long int

// Function to count total factors of N
lli CountFactors(lli N)
{
    lli cnt = 0;
    for (lli i = 1;
         i * i <= N; i++) {

        if (N % i == 0)
            cnt += ((N / i == i) ? 1 : 2);
    }

    // Return the count
    return cnt;
}

// Function to search lowest N
// such that the given condition
// is satisfied
lli minN(lli X)
{
    lli i = 1;
    lli total = 0;

    while (1) {

        // Add the count of total factor
        // of i to variable total
        total = total + CountFactors(i);

        // If total count is greater than
        // equal to N, then return i
        if (total >= X)
            return i;
        i++;
    }
}

// Driver Code
int main()
{
    // Given sum
    lli X = 10;

    // Function Call
    cout << minN(X) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class GFG{

static final int MAX = 1000050;

// Function to count total factors of N
static int CountFactors(int N)
{
    int cnt = 0;
    for(int i = 1; i * i <= N; i++)
    {
       if (N % i == 0)
           cnt += ((N / i == i) ? 1 : 2);
    }

    // Return the count
    return cnt;
}

// Function to search lowest N
// such that the given condition
// is satisfied
static int minN(int X)
{
    int i = 1;
    int total = 0;

    while (true)
    {

        // Add the count of total factor
        // of i to variable total
        total = total + CountFactors(i);

        // If total count is greater than
        // equal to N, then return i
        if (total >= X)
            return i;
        i++;
    }
}

// Driver Code
public static void main(String[] args)
{

    // Given sum
    int X = 10;

    // Function Call
    System.out.print(minN(X) + "\n");
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program for
# the above approach
MAX = 1000050

# Function to count
# total factors of N
def CountFactors(N):

    cnt = 0
    i = 1
    while i * i <= N:

        if (N % i == 0):
            if (N // i == i):
                cnt +=  1
            else:
                cnt +=  2
        i += 1  

    # Return the count
    return cnt

# Function to search lowest N
# such that the given condition
# is satisfied
def minN(X):

    i = 1
    total = 0

    while (1):

        # Add the count of total factor
        # of i to variable total
        total = total + CountFactors(i)

        # If total count is greater than
        # equal to N, then return i
        if (total >= X):
            return i
        i += 1

# Driver Code
if __name__ == "__main__":

    # Given sum
    X = 10

    # Function Call
    print( minN(X))

# This code is contributed by Chitranayal
```

## C#

```
// C# program for the above approach
using System;

class GFG{

//static readonly int MAX = 1000050;

// Function to count total factors of N
static int CountFactors(int N)
{
    int cnt = 0;
    for(int i = 1; i * i <= N; i++)
    {
       if (N % i == 0)
           cnt += ((N / i == i) ? 1 : 2);
    }

    // Return the count
    return cnt;
}

// Function to search lowest N
// such that the given condition
// is satisfied
static int minN(int X)
{
    int i = 1;
    int total = 0;

    while (true)
    {

        // Add the count of total factor
        // of i to variable total
        total = total + CountFactors(i);

        // If total count is greater than
        // equal to N, then return i
        if (total >= X)
            return i;
        i++;
    }
}

// Driver Code
public static void Main(String[] args)
{

    // Given sum
    int X = 10;

    // Function Call
    Console.Write(minN(X) + "\n");
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// javascript program for the above approachstatic final var MAX = 1000050;

// Function to count total factors of N
function CountFactors(N)
{
    var cnt = 0;
    for(i = 1; i * i <= N; i++)
    {
       if (N % i == 0)
           cnt += ((N / i == i) ? 1 : 2);
    }

    // Return the count
    return cnt;
}

// Function to search lowest N
// such that the given condition
// is satisfied
function minN(X)
{
    var i = 1;
    var total = 0;

    while (true)
    {

        // Add the count of total factor
        // of i to variable total
        total = total + CountFactors(i);

        // If total count is greater than
        // equal to N, then return i
        if (total >= X)
            return i;
        i++;
    }
}

// Driver Code
//Given sum
var X = 10;

// Function Call
document.write(minN(X) + "\n");

// This code is contributed by 29AjayKumar
</script>
```

**Output:** 

```
5
```