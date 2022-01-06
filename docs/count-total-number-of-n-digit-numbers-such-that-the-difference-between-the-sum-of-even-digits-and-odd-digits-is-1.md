# 计算 N 位数的总数，使偶数和奇数之和的差为 1

> 原文:[https://www . geeksforgeeks . org/count-n 位数的总数-数字-偶数和奇数之和的差为-1/](https://www.geeksforgeeks.org/count-total-number-of-n-digit-numbers-such-that-the-difference-between-the-sum-of-even-digits-and-odd-digits-is-1/)

给定一个数字 n，我们需要计算 n 位数的总数，使得偶数位数的总和比奇数位数的总和多 1。这里的偶数和奇数表示数字的位置类似数组索引，例如，最左边(或前导)的数字被认为是偶数，最左边旁边的数字被认为是奇数，以此类推。

**示例:**

```
Input:  n = 2
Output: Required Count of 2 digit numbers is 9
Explanation : 10, 21, 32, 43, 54, 65, 76, 87, 98.

Input:  n = 3
Output: Required Count of 3 digit numbers is 54
Explanation: 100, 111, 122, ......, 980
```

**我们强烈建议你尽量减少浏览器，先自己试试这个。**
这个问题主要是[计数 n 位数的扩展，其位数之和等于给定的和](https://www.geeksforgeeks.org/count-of-n-digit-numbers-whose-sum-of-digits-equals-to-given-sum/)。这里子问题的求解依赖于四个变量:位数、esum(当前偶和)、osum(当前奇和)、isEven(表示当前位数是偶数还是奇数的标志)。

下面是基于记忆的解决方案。

## C++

```
// A memoization based recursive program to count numbers
// with difference between odd and even digit sums as 1
#include<bits/stdc++.h>

using namespace std;

// A lookup table used for memoization.
unsigned long long int lookup[50][1000][1000][2];

// Memoization based recursive function to count numbers
// with even and odd digit sum difference as 1.  This function
// considers leading zero as a digit
unsigned long long int  countRec(int digits, int esum,
                               int osum, bool isOdd, int n)
{
    // Base Case
    if (digits == n)
        return (esum - osum == 1);

    // If current subproblem is already computed
    if (lookup[digits][esum][osum][isOdd] != -1)
        return lookup[digits][esum][osum][isOdd];

    // Initialize result
    unsigned long long int ans = 0;

    // If the current digit is odd, then add it to odd sum and recur
    if (isOdd)
      for (int i = 0; i <= 9; i++)
          ans +=  countRec(digits+1, esum, osum+i, false, n);
    else // Add to even sum and recur
      for (int i = 0; i <= 9; i++)
          ans +=  countRec(digits+1, esum+i, osum, true, n);

    // Store current result in lookup table and return the same
    return lookup[digits][esum][osum][isOdd] = ans;
}

// This is mainly a wrapper over countRec. It
// explicitly handles leading digit and calls
// countRec() for remaining digits.
unsigned long long int finalCount(int n)
{
    // Initialize number digits considered so far
    int digits = 0;

    // Initialize all entries of lookup table
    memset(lookup, -1, sizeof lookup);

    // Initialize final answer
    unsigned long long int ans = 0;

    // Initialize even and odd sums
    int esum = 0, osum = 0;

    // Explicitly handle first digit and call recursive function
    // countRec for remaining digits.  Note that the first digit
    // is considered as even digit.
    for (int i = 1; i <= 9; i++)
          ans +=  countRec(digits+1, esum + i, osum, true, n);

    return ans;
}

// Driver program
int main()
{
    int n = 3;
    cout << "Count of "<<n << " digit numbers is " << finalCount(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A memoization based recursive
// program to count numbers with
// difference between odd and
// even digit sums as 1
class GFG
{

// A lookup table used for memoization.
static int [][][][]lookup = new int[50][1000][1000][2];

// Memoization based recursive
// function to count numbers
// with even and odd digit sum
// difference as 1\. This function
// considers leading zero as a digit
static int countRec(int digits, int esum,
                            int osum, int isOdd, int n)
{
    // Base Case
    if (digits == n)
        return (esum - osum == 1)?1:0;

    // If current subproblem is already computed
    if (lookup[digits][esum][osum][isOdd] != -1)
        return lookup[digits][esum][osum][isOdd];

    // Initialize result
    int ans = 0;

    // If current digit is odd, then
    // add it to odd sum and recur
    if (isOdd==1)
    for (int i = 0; i <= 9; i++)
        ans += countRec(digits+1, esum, osum+i, 0, n);
    else // Add to even sum and recur
    for (int i = 0; i <= 9; i++)
        ans += countRec(digits+1, esum+i, osum, 1, n);

    // Store current result in lookup
    // table and return the same
    return lookup[digits][esum][osum][isOdd] = ans;
}

// This is mainly a wrapper over countRec. It
// explicitly handles leading digit and calls
// countRec() for remaining digits.
static int finalCount(int n)
{
    // Initialize number digits considered so far
    int digits = 0;

    // Initialize all entries of lookup table
    for(int i = 0; i < 50; i++)
        for(int j = 0; j < 1000; j++)
            for(int k = 0; k < 1000; k++)
                for(int l = 0; l < 2; l++)
                    lookup[i][j][k][l] = -1;

    // Initialize final answer
    int ans = 0;

    // Initialize even and odd sums
    int esum = 0, osum = 0;

    // Explicitly handle first digit and
    // call recursive function countRec
    // for remaining digits. Note that
    // the first digit is considered
    // as even digit.
    for (int i = 1; i <= 9; i++)
        ans += countRec(digits+1, esum + i, osum, 1, n);

    return ans;
}

// Driver program
public static void main(String[] args)
{
    int n = 3;
    System.out.println("Count of "+ n +
            " digit numbers is " + finalCount(n));
}
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# A memoization based recursive program to count numbers
# with difference between odd and even digit sums as 1

# Memoization based recursive function to count numbers
# with even and odd digit sum difference as 1\. This function
# considers leading zero as a digit
def countRec(digits, esum, osum, isOdd, n):

    # Base Case
    if digits == n:
        return (esum - osum == 1)

    # If current subproblem is already computed
    if lookup[digits][esum][osum][isOdd] != -1:
        return lookup[digits][esum][osum][isOdd]

    # Initialize result
    ans = 0

    # If the current digit is odd,
    # then add it to odd sum and recur
    if isOdd:
        for i in range(10):
            ans += countRec(digits + 1, esum,
                            osum + i, False, n)

    # Add to even sum and recur
    else:
        for i in range(10):
            ans += countRec(digits + 1, esum + i,
                            osum, True, n)

    # Store current result in lookup table
    # and return the same
    lookup[digits][esum][osum][isOdd] = ans
    return ans

# This is mainly a wrapper over countRec. It
# explicitly handles leading digit and calls
# countRec() for remaining digits.
def finalCount(n):
    global lookup

    # Initialize number digits considered so far
    digits = 0

    # Initialize all entries of lookup table
    lookup = [[[[-1, -1] for i in range(500)]
                         for j in range(500)]
                          for k in range(50)]

    # Initialize final answer
    ans = 0

    # Initialize even and odd sums
    esum = 0
    osum = 0

    # Explicitly handle first digit and call
    # recursive function countRec for remaining digits.
    # Note that the first digit is considered as even digit
    for i in range(1, 10):
        ans += countRec(digits + 1, esum + i,
                        osum, True, n)

    return ans

# Driver Code
if __name__ == "__main__":

    # A lookup table used for memoization.
    lookup = []
    n = 3
    print("Count of %d digit numbers is %d" % (n, finalCount(n)))

# This code is contributed by
# sanjeev2552
```

## C#

```
// A memoization based recursive
// program to count numbers with
// difference between odd and
// even digit sums as 1
using System;

class GFG
{

// A lookup table used for memoization.
static int [,,,]lookup = new int[50,1000,1000,2];

// Memoization based recursive
// function to count numbers
// with even and odd digit sum
// difference as 1\. This function
// considers leading zero as a digit
static int countRec(int digits, int esum,
                    int osum, int isOdd, int n)
{
    // Base Case
    if (digits == n)
        return (esum - osum == 1)?1:0;

    // If current subproblem is already computed
    if (lookup[digits,esum,osum,isOdd] != -1)
        return lookup[digits,esum,osum,isOdd];

    // Initialize result
    int ans = 0;

    // If current digit is odd, then
    // add it to odd sum and recur
    if (isOdd==1)
    for (int i = 0; i <= 9; i++)
        ans += countRec(digits+1, esum, osum+i, 0, n);
    else // Add to even sum and recur
    for (int i = 0; i <= 9; i++)
        ans += countRec(digits+1, esum+i, osum, 1, n);

    // Store current result in lookup
    // table and return the same
    return lookup[digits,esum,osum,isOdd] = ans;
}

// This is mainly a wrapper over countRec. It
// explicitly handles leading digit and calls
// countRec() for remaining digits.
static int finalCount(int n)
{
    // Initialize number digits considered so far
    int digits = 0;

    // Initialize all entries of lookup table
    for(int i = 0; i < 50; i++)
        for(int j = 0; j < 1000; j++)
            for(int k = 0; k < 1000; k++)
                for(int l = 0; l < 2; l++)
                    lookup[i,j,k,l] = -1;

    // Initialize final answer
    int ans = 0;

    // Initialize even and odd sums
    int esum = 0, osum = 0;

    // Explicitly handle first digit and
    // call recursive function countRec
    // for remaining digits. Note that
    // the first digit is considered
    // as even digit.
    for (int i = 1; i <= 9; i++)
        ans += countRec(digits+1, esum + i, osum, 1, n);

    return ans;
}

// Driver code
public static void Main(String[] args)
{
    int n = 3;
    Console.WriteLine("Count of "+ n +
            " digit numbers is " + finalCount(n));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// A memoization based recursive
// program to count numbers with
// difference between odd and
// even digit sums as 1

// A lookup table used for memoization.
let lookup = new Array(50);
for(let i=0;i<50;i++)
{
    lookup[i]=new Array(1000);
    for(let j=0;j<1000;j++)
    {
        lookup[i][j]=new Array(1000);
        for(let k=0;k<1000;k++)
        {
            lookup[i][j][k]=new Array(2);
        }

    }
}

// Memoization based recursive
// function to count numbers
// with even and odd digit sum
// difference as 1\. This function
// considers leading zero as a digit
function countRec(digits,esum,osum,isOdd,n)
{
    // Base Case
    if (digits == n)
        return (esum - osum == 1)?1:0;

    // If current subproblem is already computed
    if (lookup[digits][esum][osum][isOdd] != -1)
        return lookup[digits][esum][osum][isOdd];

    // Initialize result
    let ans = 0;

    // If current digit is odd, then
    // add it to odd sum and recur
    if (isOdd==1)
    for (let i = 0; i <= 9; i++)
        ans += countRec(digits+1, esum, osum+i, 0, n);
    else // Add to even sum and recur
    for (let i = 0; i <= 9; i++)
        ans += countRec(digits+1, esum+i, osum, 1, n);

    // Store current result in lookup
    // table and return the same
    return lookup[digits][esum][osum][isOdd] = ans;
}

// This is mainly a wrapper over countRec. It
// explicitly handles leading digit and calls
// countRec() for remaining digits.
function finalCount(n)
{
    // Initialize number digits considered so far
    let digits = 0;

    // Initialize all entries of lookup table
    for(let i = 0; i < 50; i++)
        for(let j = 0; j < 1000; j++)
            for(let k = 0; k < 1000; k++)
                for(let l = 0; l < 2; l++)
                    lookup[i][j][k][l] = -1;

    // Initialize final answer
    let ans = 0;

    // Initialize even and odd sums
    let esum = 0, osum = 0;

    // Explicitly handle first digit and
    // call recursive function countRec
    // for remaining digits. Note that
    // the first digit is considered
    // as even digit.
    for (let i = 1; i <= 9; i++)
        ans += countRec(digits+1, esum + i, osum, 1, n);

    return ans;
}

// Driver program
let n = 3;
document.write("Count of "+ n +
            " digit numbers is " + finalCount(n));

// This code is contributed by rag2127

</script>
```

**输出:**

```
Count of 3 digit numbers is 54
```

感谢 Gaurav Ahirwar 提供上述解决方案。

如果发现有不正确的地方，请写评论，或者想分享更多关于以上讨论话题的信息