# 用给定的数字和计算数字(小于或等于 N)

> 原文:[https://www . geesforgeks . org/count-numbers-小于或等于 n 的给定数字总和/](https://www.geeksforgeeks.org/count-numbers-smaller-than-or-equal-to-n-with-given-digit-sum/)

给定一个数 N 和一个数 S，求数 N 的和等于数 S 的个数

```
Examples:
Input : N = 100, S = 4
Output : 5
Upto 100 only 5 numbers(4, 13, 22, 31, 40)
can produce 4 as their sum of digits.

Input : N = 1000, S = 1
Output : 4
Upto 1000 only 4 numbers(1, 10, 100 and 1000) 
can produce 1 as their sum of digits.

```

我们可以做一个有状态的[数字 DP](https://www.geeksforgeeks.org/digit-dp-introduction/) (当前索引，当前构造的 I 位数是否等于或小于 N 的前 I 位构成的数，当前构造数的位数之和)。

设 DP[I][紧密][sum_so_far]表示前 I 位已被考虑的数的计数，紧密表示当前构造的数是否等于或小于由 n 的前 I 位构成的数。如果紧密为真，则表示当前构造的数等于由 n 的前 I 位构成的数。如果为假，则表示当前构造的数小于由 n 的前 I 位构成的数。sum_so_far 表示当前构造的数的位数之和。

**基本情况:**
如果 I = N 中的位数，sum_so_far = Sum，那么答案= 1，否则答案为 0。

**Transitions:**
对于填充第(i+1)个数字，我们可以考虑如下–
如果紧密为真，那么这意味着我们构造的数字仍然等于由 N 的前 I 个数字形成的数字。我们可以尝试我们当前可能的数字值，从 0 到 N 的第(i+1)个数字。如果我们尝试的数字多于第(i+1)个数字，那么构造的数字将变得大于由 N 的前 I 个数字形成的数字， 这就违反了我们构造的数应该是< = N.
的性质，如果紧是假的，那么这意味着从第一个 I–1 位构造的数变得小于从第一个 I–1 位构造的数，所以这意味着我们的数永远不能超过 N，所以我们可以选择从 0 到 9 的任意一位。
nsum_so_far 可以通过 sum_so_far 和当前数字(currdigit)相加得到。

最后，我们将返回一个答案，即数字总和等于 s 的数的计数。

## C++

```
#include <bits/stdc++.h>
using namespace std;

// N can be max 10^18 and hence digitsum will be 162 maximum.
long long dp[18][2][162];

long long solve(int i, bool tight, int sum_so_far,
                int Sum, string number, int len)
{
    if (i == len) {

        // If sum_so_far equals to given sum then 
        // return 1 else 0
        if (sum_so_far == Sum)
            return 1;
        else
            return 0;
    }

    long long& ans = dp[i][tight][sum_so_far];
    if (ans != -1) {
        return ans;
    }

    ans = 0;
    bool ntight;
    int nsum_so_far;
    for (char currdigit = '0'; currdigit <= '9'; currdigit++) {

        // Our constructed number should not become
        // greater than N.
        if (!tight && currdigit > number[i]) {
            break;
        }

        // If tight is true then it will also be true for (i+1) digit.
        ntight = tight || currdigit < number[i];
        nsum_so_far = sum_so_far + (currdigit - '0');
        ans += solve(i + 1, ntight, nsum_so_far, Sum, number, len);
    }

    return ans;
}

// Driver code
int main()
{
    long long count = 0;
    long long sum = 4;
    string number = "100";
    memset(dp, -1, sizeof dp);
    cout << solve(0, 0, 0, sum, number, number.size());
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count 2s from 0 to n 
class GFG 
{

// N can be max 10^18 and hence 
// digitsum will be 162 maximum. 
static long dp[][][] = new long[18][2][162]; 

static long solve(int i, boolean tight, int sum_so_far, 
                int Sum, String number, int len) 
{ 
    if (i == len) 
    { 

        // If sum_so_far equals to given sum then 
        // return 1 else 0 
        if (sum_so_far == Sum) 
            return 1; 
        else
            return 0; 
    } 

    long ans = dp[i][1][sum_so_far]; 
    if (ans != -1) 
    { 
        return ans; 
    } 

    ans = 0; 
    boolean ntight; 
    int nsum_so_far; 
    for (char currdigit = '0'; currdigit <= '9'; currdigit++) 
    { 

        // Our constructed number should not become 
        // greater than N. 
        if (!tight && currdigit > number.charAt(i))
        { 
            break; 
        } 

        // If tight is true then it will 
        // also be true for (i+1) digit. 
        ntight = tight || currdigit < number.charAt(i); 
        nsum_so_far = sum_so_far + (currdigit - '0'); 
        ans += solve(i + 1, ntight, nsum_so_far, 
                        Sum, number, len); 
    } 
    return ans; 
} 

// Driver code 
public static void main(String[] args) 
{
    long count = 0; 
    int sum = 4; 
    String number = "100"; 
    for(int i = 0; i < 18; i++)
    {
        for(int j = 0; j < 2; j++)
        {
            for(int k = 0; k < 162; k++)
            dp[i][j][k] = -1;
        }
    }
    System.out.println( solve(0, false, 0, sum, 
                        number, number.length())); 
    }
} 

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of the given approach. 

def solve(i, tight, sum_so_far, Sum, number, length): 

    if i == length: 

        # If sum_so_far equals to given 
        # sum then return 1 else 0 
        if sum_so_far == Sum: 
            return 1
        else:
            return 0

    ans = dp[i][tight][sum_so_far] 
    if ans != -1: 
        return ans 

    ans = 0
    for currdigit in range(0, 10): 

        currdigitstr = str(currdigit)

        # Our constructed number should 
        # not become greater than N. 
        if not tight and currdigitstr > number[i]: 
            break

        # If tight is true then it will also be true for (i+1) digit. 
        ntight = tight or currdigitstr < number[i] 
        nsum_so_far = sum_so_far + currdigit 
        ans += solve(i + 1, ntight, nsum_so_far, Sum, number, length) 

    return ans 

# Driver code 
if __name__ == "__main__":

    count, Sum = 0, 4
    number = "100"
    dp = [[[-1 for i in range(162)] for j in range(2)] for k in range(18)]
    print(solve(0, 0, 0, Sum, number, len(number)))

# This code is contributed by Rituraj Jain
```

## C#

```
// C# program to count 2s from 0 to n 
using System;

class GFG 
{ 

    // N can be max 10^18 and hence 
    // digitsum will be 162 maximum. 
    static long [ , , ]dp = new long[18,2,162]; 

    static long solve(int i, bool tight, int sum_so_far, 
                    int Sum, String number, int len) 
    { 
        if (i == len) 
        { 

            // If sum_so_far equals to given sum then 
            // return 1 else 0 
            if (sum_so_far == Sum) 
                return 1; 
            else
                return 0; 
        } 

        long ans = dp[i,1,sum_so_far]; 
        if (ans != -1) 
        { 
            return ans; 
        } 

        ans = 0; 
        bool ntight; 
        int nsum_so_far; 
        for (char currdigit = '0'; currdigit <= '9'; currdigit++) 
        { 

            // Our constructed number should not become 
            // greater than N. 
            if (!tight && currdigit > number[i]) 
            { 
                break; 
            } 

            // If tight is true then it will 
            // also be true for (i+1) digit. 
            ntight = tight || currdigit < number[i]; 
            nsum_so_far = sum_so_far + (currdigit - '0'); 
            ans += solve(i + 1, ntight, nsum_so_far, 
                            Sum, number, len); 
        } 
        return ans; 
    } 

    // Driver code 
    public static void Main(String[] args) 
    { 
        int sum = 4; 
        String number = "100"; 
        for(int i = 0; i < 18; i++) 
        { 
            for(int j = 0; j < 2; j++) 
            { 
                for(int k = 0; k < 162; k++) 
                dp[i,j,k] = -1; 
            } 
        } 
        Console.WriteLine( solve(0, false, 0, sum, 
                            number, number.Length)); 
        } 
} 

// This code has been contributed by Rajput-Ji
```

**Output:**

```
5

```

**时间复杂度:** 2(紧)* Sum * log 10(N) * 10(跃迁)= 20*log 10(N)*Sum。