# 第一个数字等于数字最后一个数字的范围内的数字计数

> 原文:[https://www . geesforgeks . org/范围内数字的计数，其中第一个数字等于数字的最后一个数字/](https://www.geeksforgeeks.org/count-of-numbers-in-range-where-first-digit-is-equal-to-last-digit-of-the-number/)

给定一个由两个正整数 L 和 r 表示的范围，求该范围内第一个数字等于最后一个数字的数字计数。

**示例:**

```
Input : L = 2, R = 60
Output : 13
Explanation : Required numbers are 
2, 3, 4, 5, 6, 7, 8, 9, 11, 22, 33, 44 and 55

Input : L = 1, R = 1000
Output : 108
```

**先决条件** : [数字 DP](https://www.geeksforgeeks.org/digit-dp-introduction/)
解决这类问题可以有两种方法，一种是组合解法，另一种是基于动态规划的解法。下面是使用数字动态编程解决这个问题的详细方法。

**动态规划解法:**首先，如果我们能够将所需的数字计数到 R，即在[0，R]的范围内，那么我们可以很容易地通过从 0 到 R 求解，然后减去从 0 到 L–1 求解后得到的答案，从而得出我们在[L，R]范围内的答案。现在，我们需要定义 DP 状态。

**差压状态**:

*   既然我们可以把我们的数字看作一个数字序列，那么一个状态就是我们当前所处的 ***位置*** 。如果我们处理的数字高达 10 <sup>18</sup> ，则该位置的值可以从 0 到 18。在每次递归调用中，我们试图通过放置一个从 0 到 9 的数字从左到右构建序列。
*   第二个状态是 ***firstD*** ，它定义了我们试图构建的数字的第一个数字，可以有从 0 到 9 的值。
*   第三个状态是 ***lastD*** ，它定义了我们试图构建的数字的最后一位，可以有 0 到 9 的值。
*   另一个状态是布尔变量**，它告诉我们试图构建的数字已经变得比 R 小，因此在即将到来的递归调用中，我们可以放置从 0 到 9 的任何数字。如果数字没有变小，我们可以放置的最大位数限制是 r 中当前位置的位数。**

**在每次递归调用中，我们将最后一个数字设置为放在最后一个位置的数字，并将第一个数字设置为数字的第一个非零数字。在最后一次递归调用中，当我们在最后一个位置时，如果第一个数字等于最后一个数字，返回 1，否则返回 0。**

**下面是上述方法的实现。**

## **C++**

```
// C++ Program to find the count of
// numbers in a range where the number
// does not contain more than K non
// zero digits

#include <bits/stdc++.h>

using namespace std;

const int M = 20;

// states - position, first digit,
// last digit, tight
int dp[M][M][M][2];

// This function returns the count of
// required numbers from 0 to num
int count(int pos, int firstD, int lastD,
        int tight, vector<int> num)
{
    // Last position
    if (pos == num.size()) {

        // If first digit is equal to
        // last digit
        if (firstD == lastD)
            return 1;
        return 0;
    }

    // If this result is already computed
    // simply return it
    if (dp[pos][firstD][lastD][tight] != -1)
        return dp[pos][firstD][lastD][tight];

    int ans = 0;

    // Maximum limit upto which we can place
    // digit. If tight is 1, means number has
    // already become smaller so we can place
    // any digit, otherwise num[pos]
    int limit = (tight ? 9 : num[pos]);

    for (int dig = 0; dig <= limit; dig++) {
        int currFirst = firstD;

        // If the position is 0, current
        // digit can be first digit
        if (pos == 0)
            currFirst = dig;

        // In current call, if the first
        // digit is zero and current digit
        // is nonzero, update currFirst
        if (!currFirst && dig)
            currFirst = dig;

        int currTight = tight;

        // At this position, number becomes
        // smaller
        if (dig < num[pos])
            currTight = 1;

        // Next recursive call, set last
        // digit as dig
        ans += count(pos + 1, currFirst,
                    dig, currTight, num);
    }
    return dp[pos][firstD][lastD][tight] = ans;
}

// This function converts a number into its
// digit vector and uses above function to compute
// the answer
int solve(int x)
{
    vector<int> num;
    while (x) {
        num.push_back(x % 10);
        x /= 10;
    }
    reverse(num.begin(), num.end());

    // Initialize dp
    memset(dp, -1, sizeof(dp));
    return count(0, 0, 0, 0, num);
}

// Driver Code
int main()
{
    int L = 2, R = 60;
    cout << solve(R) - solve(L - 1) << endl;

    L = 1, R = 1000;
    cout << solve(R) - solve(L - 1) << endl;

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program to find the count of
// numbers in a range where the number
// does not contain more than K non
// zero digits
import java.util.Collections;
import java.util.Vector;

class GFG
{
    static int M = 20;

    // states - position, first digit,
    // last digit, tight
    static int[][][][] dp = new int[M][M][M][2];

    // This function returns the count of
    // required numbers from 0 to num
    static int count(int pos, int firstD,
                     int lastD, int tight,
                     Vector<Integer> num)
    {

        // Last position
        if (pos == num.size())
        {

            // If first digit is equal to
            // last digit
            if (firstD == lastD)
                return 1;
            return 0;
        }

        // If this result is already computed
        // simply return it
        if (dp[pos][firstD][lastD][tight] != -1)
            return dp[pos][firstD][lastD][tight];
        int ans = 0;

        // Maximum limit upto which we can place
        // digit. If tight is 1, means number has
        // already become smaller so we can place
        // any digit, otherwise num[pos]
        int limit = (tight == 1 ? 9 : num.elementAt(pos));

        for (int dig = 0; dig <= limit; dig++)
        {
            int currFirst = firstD;

            // If the position is 0, current
            // digit can be first digit
            if (pos == 0)
                currFirst = dig;

            // In current call, if the first
            // digit is zero and current digit
            // is nonzero, update currFirst
            if (currFirst == 0 && dig != 0)
                currFirst = dig;

            int currTight = tight;

            // At this position, number becomes
            // smaller
            if (dig < num.elementAt(pos))
                currTight = 1;

            // Next recursive call, set last
            // digit as dig
            ans += count(pos + 1, currFirst,
                         dig, currTight, num);
        }
        return dp[pos][firstD][lastD][tight] = ans;
    }

    // This function converts a number into its
    // digit vector and uses above function to
    // compute the answer
    static int solve(int x)
    {
        Vector<Integer> num = new Vector<>();
        while (x > 0)
        {
            num.add(x % 10);
            x /= 10;
        }

        Collections.reverse(num);

        // Initialize dp
        for (int i = 0; i < M; i++)
            for (int j = 0; j < M; j++)
                for (int k = 0; k < M; k++)
                    for (int l = 0; l < 2; l++)
                        dp[i][j][k][l] = -1;

        return count(0, 0, 0, 0, num);
    }

    // Driver Code
    public static void main(String[] args)
    {
        int L = 2, R = 60;
        System.out.println(solve(R) - solve(L - 1));

        L = 1;
        R = 1000;
        System.out.println(solve(R) - solve(L - 1));
    }
}

// This code is contributed by
// sanjeev2552
```

## **蟒蛇 3**

```
# Python3 code for above approach

# Returns the count of numbers in range
# if the first digit is equal to last digit of number
def count(l, r):
    cnt = 0       # Initialize counter
    for i in range(l, r):

        # If number is less than 10
        # then increment counter
        # as number has only one digit
        if(i < 10):    
            cnt += 1

        else:
            n = i % 10     # Find the last digit
            k = i

            # Find the first digit
            while(k >= 10):
                k = k // 10

            # If first digit equals last digit
            # then increment counter
            if(n == k):
                cnt += 1

    return(cnt)     # Return the count

# Driver Code
L = 2; R = 60;
print(count(L, R))

L = 1; R = 1000;
print(count(L, R))

# This code is contributed by Raj
```

## **C#**

```
// C# program to find the count of
// numbers in a range where the number
// does not contain more than K non
// zero digits
using System;
using System.Collections.Generic;            

class GFG
{
    static int M = 20;

    // states - position, first digit,
    // last digit, tight
    static int[,,,] dp = new int[M, M, M, 2];

    // This function returns the count of
    // required numbers from 0 to num
    static int count(int pos, int firstD,
                     int lastD, int tight,
                     List<int> num)
    {

        // Last position
        if (pos == num.Count)
        {

            // If first digit is equal to
            // last digit
            if (firstD == lastD)
                return 1;
            return 0;
        }

        // If this result is already computed
        // simply return it
        if (dp[pos, firstD, lastD, tight] != -1)
            return dp[pos, firstD, lastD, tight];
        int ans = 0;

        // Maximum limit upto which we can place
        // digit. If tight is 1, means number has
        // already become smaller so we can place
        // any digit, otherwise num[pos]
        int limit = (tight == 1 ? 9 : num[pos]);

        for (int dig = 0; dig <= limit; dig++)
        {
            int currFirst = firstD;

            // If the position is 0, current
            // digit can be first digit
            if (pos == 0)
                currFirst = dig;

            // In current call, if the first
            // digit is zero and current digit
            // is nonzero, update currFirst
            if (currFirst == 0 && dig != 0)
                currFirst = dig;

            int currTight = tight;

            // At this position, number becomes
            // smaller
            if (dig < num[pos])
                currTight = 1;

            // Next recursive call, set last
            // digit as dig
            ans += count(pos + 1, currFirst,
                         dig, currTight, num);
        }
        return dp[pos, firstD, lastD, tight] = ans;
    }

    // This function converts a number into its
    // digit vector and uses above function to
    // compute the answer
    static int solve(int x)
    {
        List<int> num = new List<int>();
        while (x > 0)
        {
            num.Add(x % 10);
            x /= 10;
        }

        num.Reverse();

        // Initialize dp
        for (int i = 0; i < M; i++)
            for (int j = 0; j < M; j++)
                for (int k = 0; k < M; k++)
                    for (int l = 0; l < 2; l++)
                        dp[i, j, k, l] = -1;

        return count(0, 0, 0, 0, num);
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int L = 2, R = 60;
        Console.WriteLine(solve(R) - solve(L - 1));

        L = 1;
        R = 1000;
        Console.WriteLine(solve(R) - solve(L - 1));
    }
}

// This code is contributed by 29AjayKumar
```

## **java 描述语言**

```
<script>

// Javascript program to find the count of
// numbers in a range where the number
// does not contain more than K non
// zero digits

let  M = 20;

// states - position, first digit,
    // last digit, tight
let dp = new Array(M);
for(let i=0;i<M;i++)
{
    dp[i]=new Array(M);
    for(let j=0;j<M;j++)
    {
        dp[i][j]=new Array(M);
        for(let k=0;k<M;k++)
            dp[i][j][k]=new Array(2);
    }
}

// This function returns the count of
    // required numbers from 0 to num
function count(pos,firstD,lastD,tight, num)
{
    // Last position
        if (pos == num.length)
        {

            // If first digit is equal to
            // last digit
            if (firstD == lastD)
                return 1;
            return 0;
        }

        // If this result is already computed
        // simply return it
        if (dp[pos][firstD][lastD][tight] != -1)
            return dp[pos][firstD][lastD][tight];
        let ans = 0;

        // Maximum limit upto which we can place
        // digit. If tight is 1, means number has
        // already become smaller so we can place
        // any digit, otherwise num[pos]
        let limit = (tight == 1 ? 9 : num[pos]);

        for (let dig = 0; dig <= limit; dig++)
        {
            let currFirst = firstD;

            // If the position is 0, current
            // digit can be first digit
            if (pos == 0)
                currFirst = dig;

            // In current call, if the first
            // digit is zero and current digit
            // is nonzero, update currFirst
            if (currFirst == 0 && dig != 0)
                currFirst = dig;

            let currTight = tight;

            // At this position, number becomes
            // smaller
            if (dig < num[pos])
                currTight = 1;

            // Next recursive call, set last
            // digit as dig
            ans += count(pos + 1, currFirst,
                         dig, currTight, num);
        }
        return dp[pos][firstD][lastD][tight] = ans;
}

// This function converts a number into its
    // digit vector and uses above function to
    // compute the answer
function solve(x)
{
    let num = [];
        while (x > 0)
        {
            num.push(x % 10);
            x = Math.floor(x/10);
        }

        num.reverse();

        // Initialize dp
        for (let i = 0; i < M; i++)
            for (let j = 0; j < M; j++)
                for (let k = 0; k < M; k++)
                    for (let l = 0; l < 2; l++)
                        dp[i][j][k][l] = -1;

        return count(0, 0, 0, 0, num);
}

// Driver Code
let L = 2, R = 60;
document.write(solve(R) - solve(L - 1)+"<br>");

L = 1;
R = 1000;
document.write(solve(R) - solve(L - 1)+"<br>");

// This code is contributed by rag2127

</script>
```

****Output**

```
13
108
```** 

****时间复杂度:** O(18 * 10 * 10 * 2 * 10)，如果我们处理的数字是 10 <sup>18</sup>** 

### ****替代方法:****

**我们也可以通过递归来解决这个问题，对于每个位置，我们可以填充任何满足给定条件的数字，除了第一个和最后一个位置，因为它们将配对在一起，为此，我们将使用递归，在每次调用中，只需检查第一个数字是否小于或大于最后一个数字，如果结果大于，我们将添加 8，否则为 9，并调用 number / 10，一旦数字首先小于 10，最后一个数字变得相同，则返回数字本身。**

**下面是上述方法的实现**

## **C++**

```
// C++ program to implement
// the above approach
#include <iostream>
using namespace std;

int solve(int x)
{

    int ans = 0, first, last, temp = x;

    // Base Case

    if (x < 10)
        return x;

    // Calculating the last digit
    last = x % 10;

    // Calculating the first digit
    while (x) {
        first = x % 10;
        x /= 10;
    }

    if (first <= last)
        ans = 9 + temp / 10;
    else
        ans = 8 + temp / 10;

    return ans;
}

// Drivers Code
int main()
{

    int L = 2, R = 60;
    cout << solve(R) - solve(L - 1) << endl;

    L = 1, R = 1000;
    cout << solve(R) - solve(L - 1) << endl;

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program to implement
// the above approach
class GFG{

public static int solve(int x)
{
  int ans = 0, first = 0,
      last, temp = x;

  // Base Case
  if (x < 10)
    return x;

  // Calculating the
  // last digit
  last = x % 10;

  // Calculating the
  // first digit
  while (x != 0)
  {
    first = x % 10;
    x /= 10;
  }

  if (first <= last)
    ans = 9 + temp / 10;
  else
    ans = 8 + temp / 10;

  return ans;
}

// Driver code
public static void main(String[] args)
{
  int L = 2, R = 60;
  System.out.println(solve(R) -
                     solve(L - 1));

  L = 1; R = 1000;
  System.out.println(solve(R) -
                     solve(L - 1));
}
}

// This code is contributed by divyeshrabadiya07
```

## **蟒蛇 3**

```
# Python3 program to implement
# the above approach
def solve(x):

    ans, temp = 0, x

    # Base Case
    if (x < 10):
        return x

    # Calculating the last digit
    last = x % 10

    # Calculating the first digit
    while (x):
        first = x % 10
        x = x // 10

    if (first <= last):
        ans = 9 + temp // 10
    else:
        ans = 8 + temp // 10

    return ans

# Driver Code
L, R = 2, 60
print(solve(R) - solve(L - 1))

L, R = 1, 1000
print(solve(R) - solve(L - 1))

# This code is contributed by divyesh072019
```

## **C#**

```
// C# program to implement
// the above approach
using System;

class GFG{

public static int solve(int x)
{
    int ans = 0, first = 0,
        last, temp = x;

    // Base Case
    if (x < 10)
        return x;

    // Calculating the
    // last digit
    last = x % 10;

    // Calculating the
    // first digit
    while (x != 0)
    {
        first = x % 10;
        x /= 10;
    }

    if (first <= last)
        ans = 9 + temp / 10;
    else
        ans = 8 + temp / 10;

    return ans;
}

// Driver code
public static void Main(String[] args)
{
    int L = 2, R = 60;
    Console.WriteLine(solve(R) -
                      solve(L - 1));

    L = 1; R = 1000;
    Console.WriteLine(solve(R) -
                      solve(L - 1));
}
}

// This code is contributed by shivanisinghss2110
```

## **java 描述语言**

```
<script>
    // Javascript program to implement
    // the above approach
    function solve(x)
    {

        let ans = 0, first, last, temp = x;

        // Base Case

        if (x < 10)
            return x;

        // Calculating the last digit
        last = x % 10;

        // Calculating the first digit
        while (x > 0)
        {
            first = x % 10;
            x /= 10;
        }

        if (first <= last)
            ans = 9 + temp / 10;
        else
            ans = 8 + temp / 10;

        return ans;
    }

    let L = 2, R = 60;
    document.write((solve(R) - solve(L - 1)) + "</br>");

    L = 1, R = 1000;
    document.write(solve(R) - solve(L - 1));

    // This code is contributed by suresh07.
</script>
```

****Output**

```
13
108
```**