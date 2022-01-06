# 将给定数字分割成质数段的方法计数

> 原文:[https://www . geeksforgeeks . org/将给定数字拆分为质数段的方法计数/](https://www.geeksforgeeks.org/count-of-ways-to-split-a-given-number-into-prime-segments/)

给定数值字符串 **str** ，任务是统计给定字符串可以拆分的方式数，使得每个段都是一个质数。因为答案可能很大，所以以 **10 <sup>9</sup> + 7** 为模返回答案。
***注**:包含前导零数字的拆分将无效，初始字符串不包含前导零。*
**示例:**

> **输入:** str = "3175"
> **输出:** 3
> **说明:**
> 有 3 种方法可以将这个字符串拆分成质数，分别是(31，7，5)，(3，17，5)，(317，5)。
> **输入:** str = "11373"
> **输出:** 6
> **解释:**
> 将此字符串拆分为质数的方法有 6 种，分别是(11，3，7，3)，(113，7，3)，(11，37，3)，(11，3，73)，(113，73)和(11，373)。

**天真法:**解决上面提到的问题，天真法就是用[递归](https://www.geeksforgeeks.org/recursion/)。

*   从给定字符串的结束索引开始递归，并考虑每一个不超过 6 位的后缀(假设质数必须在**【1，10<sup>6</sup>)】**的范围内)，并检查它是否是质数。
*   如果后缀不包含前导零，并且它是一个质数，那么递归调用该函数来计算剩余字符串的路数，并添加到总计数中。
*   当索引达到 0 时，我们达到基本情况并返回 1，将当前拆分视为有效计数。
*   对每次迭代的计数取模，并在最后返回计数。

下面是上面的实现方法:

## C++

```
// C++ implementation to count total
// number of ways to split a
// string to get prime numbers

#include <bits/stdc++.h>
using namespace std;
#define MOD 1000000007

// Function to check whether a number
// is a prime number or not
bool isPrime(string number)
{
    int num = stoi(number);
    for (int i = 2; i * i <= num; i++)
        if ((num % i) == 0)
            return false;
    return num > 1 ? true : false;
}

// Function to find the count
// of ways to split string
// into prime numbers
int countPrimeStrings(
    string& number, int i)
{

    // 1 based indexing
    if (i == 0)
        return 1;
    int cnt = 0;

    // Consider every suffix up to 6 digits
    for (int j = 1; j <= 6; j++) {

        // Number should not have
        // a leading zero and
        // it should be a prime number
        if (i - j >= 0
            && number[i - j] != '0'
            && isPrime(
                   number.substr(i - j, j))) {
            cnt
                += countPrimeStrings(
                    number,
                    i - j);

            cnt %= MOD;
        }
    }

    // Return the final result
    return cnt;
}

// Driver code
int main()
{
    string s1 = "3175";

    int l = s1.length();
    cout << countPrimeStrings(s1, l);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to count total
// number of ways to split a string
// to get prime numbers
import java.util.*;

class GFG{

static final int MOD =1000000007;

// Function to check whether a number
// is a prime number or not
static boolean isPrime(String number)
{
    int num = Integer.valueOf(number);

    for(int i = 2; i * i <= num; i++)
    {
       if ((num % i) == 0)
           return false;
    }
    return num > 1 ? true : false;
}

// Function to find the count
// of ways to split String
// into prime numbers
static int countPrimeStrings(String number,
                                     int i)
{

    // 1 based indexing
    if (i == 0)
        return 1;

    int cnt = 0;

    // Consider every suffix up to 6 digits
    for(int j = 1; j <= 6; j++)
    {

       // Number should not have
       // a leading zero and it
       // should be a prime number
       if (i - j >= 0 &&
           number.charAt(i - j) != '0' &&
           isPrime(number.substring(i - j, i)))
       {
           cnt += countPrimeStrings(number,
                                    i - j);
           cnt %= MOD;
       }
    }

    // Return the final result
    return cnt;
}

// Driver code
public static void main(String[] args)
{
    String s1 = "3175";
    int l = s1.length();

    System.out.print(countPrimeStrings(s1, l));
}
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python3 implementation to
# count total number of ways
# to split a string to get
# prime numbers
MOD = 1000000007

# Function to check whether
# a number is a prime number
# or not
def isPrime(number):

    num = int(number)
    i = 2

    while i * i <= num:
        if ((num % i) == 0):
            return False
        i += 1

    if num > 1:
      return True
    else:
      return False

# Function to find the count
# of ways to split string
# into prime numbers
def countPrimeStrings(number, i):

    # 1 based indexing
    if (i == 0):
        return 1
    cnt = 0

    # Consider every suffix
    # up to 6 digits
    for j in range(1, 7):

        # Number should not have
        # a leading zero and
        # it should be a prime number
        if (i - j >= 0 and
            number[i - j] != '0' and
            isPrime(number[i - j : i])):
            cnt += countPrimeStrings(number,
                                     i - j)
            cnt %= MOD

    # Return the final result
    return cnt

# Driver code
if __name__ == "__main__":

    s1 = "3175"
    l = len(s1)
    print (countPrimeStrings(s1, l))

# This code is contributed by Chitranayal
```

## C#

```
// C# implementation to count total
// number of ways to split a string
// to get prime numbers
using System;
class GFG{

static readonly int MOD =1000000007;

// Function to check whether a number
// is a prime number or not
static bool isPrime(String number)
{
    int num = Int32.Parse(number);

    for(int i = 2; i * i <= num; i++)
    {
        if ((num % i) == 0)
            return false;
    }
    return num > 1 ? true : false;
}

// Function to find the count
// of ways to split String
// into prime numbers
static int countPrimeStrings(String number,
                                     int i)
{

    // 1 based indexing
    if (i == 0)
        return 1;

    int cnt = 0;

    // Consider every suffix up to 6 digits
    for(int j = 1; j <= 6; j++)
    {

        // Number should not have
        // a leading zero and it
        // should be a prime number
        if (i - j >= 0 &&
            number[i - j] != '0' &&
            isPrime(number.Substring(i - j, j)))
        {
            cnt += countPrimeStrings(number,
                                     i - j);
            cnt %= MOD;
        }
    }

    // Return the readonly result
    return cnt;
}

// Driver code
public static void Main(String[] args)
{
    String s1 = "3175";
    int l = s1.Length;

    Console.Write(countPrimeStrings(s1, l));
}
}

// This code is contributed by sapnasingh4991
```

## java 描述语言

```
<script>
// Javascript implementation to count total
// number of ways to split a string
// to get prime numbers

let MOD =1000000007;
// Function to check whether a number
// is a prime number or not
function isPrime(number)
{
    let num = parseInt(number);

    for(let i = 2; i * i <= num; i++)
    {
       if ((num % i) == 0)
           return false;
    }
    return num > 1 ? true : false;
}

// Function to find the count
// of ways to split String
// into prime numbers
function countPrimeStrings(number,i)
{
    // 1 based indexing
    if (i == 0)
        return 1;

    let cnt = 0;

    // Consider every suffix up to 6 digits
    for(let j = 1; j <= 6; j++)
    {

       // Number should not have
       // a leading zero and it
       // should be a prime number
       if (i - j >= 0 &&
           number[i - j] != '0' &&
           isPrime(number.substring(i - j, i)))
       {
           cnt += countPrimeStrings(number,
                                    i - j);
           cnt %= MOD;
       }
    }

    // Return the final result
    return cnt;
}

// Driver code
let s1 = "3175";
let l = s1.length;
document.write(countPrimeStrings(s1, l));

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
3
```

**时间复杂度:***O(N<sup>2</sup>)*
**辅助空间:** *O(N)*
**高效途径:**优化上述方法的主要思想是使用**记忆化技术**来降低上述递归解的时间复杂度。让我们考虑一个 **dp[]** 表，它在每个索引 **dp[i]** 处存储字符串 **str** 的第一个 **i** 数字的拆分方法。使用厄拉多塞的[筛可以进一步降低检查一个数是否为素数的复杂度。
以下是上述方法的实施:](https://www.geeksforgeeks.org/sieve-of-eratosthenes/) 

## C++

```
// C++ implementation to count total
// number of ways to split a
// string to get prime numbers

#include <bits/stdc++.h>
using namespace std;
const int MOD = 1000000007;
bool sieve[1000000];

// Function to build sieve
void buildSieve()
{
    for (auto& i : sieve)
        i = true;

    sieve[0] = false;
    sieve[1] = false;

    for (int p = 2; p * p <= 1000000;
         p++) {

        // If p is a prime
        if (sieve[p] == true) {

            // Update all multiples
            // of p as non prime

            for (int i = p * p; i <= 1000000;
                 i += p)
                sieve[i] = false;
        }
    }
}

// Function to check whether a number
// is a prime number or not
bool isPrime(string number)
{
    int num = stoi(number);
    return sieve[num];
}

// Function to find the count
// of ways to split string
// into prime numbers
int rec(string& number, int i,
        vector<int>& dp)
{
    if (dp[i] != -1)
        return dp[i];

    int cnt = 0;

    for (int j = 1; j <= 6; j++) {

        // Number should not have a
        // leading zero and it
        // should be a prime number
        if (i - j >= 0
            && number[i - j] != '0'
            && isPrime(
                   number.substr(i - j, j))) {

            cnt += rec(
                number, i - j, dp);
            cnt %= MOD;
        }
    }
    return dp[i] = cnt;
}

// Function to count the
// number of prime strings
int countPrimeStrings(string& number)
{
    int n = number.length();
    vector<int> dp(n + 1, -1);
    dp[0] = 1;
    return rec(number, n, dp);
}

// Driver code
int main()
{
    buildSieve();

    string s1 = "3175";

    cout << countPrimeStrings(s1) << "\n";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to count total
// number of ways to split a String
// to get prime numbers
import java.util.*;

class GFG{

static int MOD = 1000000007;
static boolean []sieve = new boolean[1000000];

// Function to build sieve
static void buildSieve()
{
    Arrays.fill(sieve, true);

    sieve[0] = false;
    sieve[1] = false;

    for(int p = 2; p * p <= 1000000; p++)
    {

       // If p is a prime
       if (sieve[p] == true)
       {

           // Update all multiples
           // of p as non prime
           for(int i = p * p; i < 1000000;
                   i += p)
              sieve[i] = false;
       }
    }
}

// Function to check whether a number
// is a prime number or not
static boolean isPrime(String number)
{
    int num = Integer.valueOf(number);
    return sieve[num];
}

// Function to find the count
// of ways to split String
// into prime numbers
static int rec(String number, int i,
                              int []dp)
{
    if (dp[i] != -1)
        return dp[i];
    int cnt = 0;

    for(int j = 1; j <= 6; j++)
    {

       // Number should not have a
       // leading zero and it
       // should be a prime number
       if (i - j >= 0 &&
           number.charAt(i - j) != '0' &&
           isPrime(number.substring(i - j, i)))
       {
           cnt += rec(number, i - j, dp);
           cnt %= MOD;
       }
    }
    return dp[i] = cnt;
}

// Function to count the
// number of prime Strings
static int countPrimeStrings(String number)
{
    int n = number.length();
    int []dp = new int[n + 1];

    Arrays.fill(dp, -1);
    dp[0] = 1;

    return rec(number, n, dp);
}

// Driver code
public static void main(String[] args)
{
    buildSieve();

    String s1 = "3175";

    System.out.print(countPrimeStrings(s1) + "\n");
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation to count total
# number of ways to split a String
# to get prime numbers
MOD = 1000000007
sieve = [0]*(1000000)

# Function to build sieve
def buildSieve():
    for i in range(len(sieve)):
        sieve[i] = True

    sieve[0] = False
    sieve[1] = False

    p = 2
    while p*p <= 1000000:
        # If p is a prime
        if sieve[p] == True:
            # Update all multiples
            # of p as non prime
            for i in range(p*p, 1000000, p):
                sieve[i] = False
        p+=1

# Function to check whether a number
# is a prime number or not
def isPrime(number):
    num = int(number)
    return sieve[num]

# Function to find the count
# of ways to split String
# into prime numbers
def rec(number,i,dp):
    if dp[i] != -1:
        return dp[i]
    cnt = 0

    for j in range(1, 7):
       # Number should not have a
       # leading zero and it
       # should be a prime number
       if (i - j) >= 0 and number[i - j] != '0' and isPrime(number[i - j: i]):
           cnt += rec(number, i - j, dp)
           cnt %= MOD
    dp[i] = cnt
    return dp[i]

# Function to count the
# number of prime Strings
def countPrimeStrings(number):
    n = len(number)
    dp = [0]*(n + 1)

    for i in range(n + 1):
        dp[i] = -1

    dp[0] = 1

    return rec(number, n, dp)

# Driver code
buildSieve()
s1 = "3175"
print(countPrimeStrings(s1))

# This code is contributed by suresh07.
```

## C#

```
// C# implementation to count total
// number of ways to split a String
// to get prime numbers
using System;

class GFG{

static int MOD = 1000000007;
static bool []sieve = new bool[1000000];

// Function to build sieve
static void buildSieve()
{
    for(int j = 0; j < sieve.Length; j++)
       sieve[j] = true;

    sieve[0] = false;
    sieve[1] = false;

    for(int p = 2; p * p <= 1000000; p++)
    {

       // If p is a prime
       if (sieve[p] == true)
       {

           // Update all multiples
           // of p as non prime
           for(int i = p * p; i < 1000000;
                   i += p)
              sieve[i] = false;
       }
    }
}

// Function to check whether a number
// is a prime number or not
static bool isPrime(String number)
{
    int num = Int32.Parse(number);
    return sieve[num];
}

// Function to find the count
// of ways to split String
// into prime numbers
static int rec(String number, int i,
                              int []dp)
{
    if (dp[i] != -1)
        return dp[i];
    int cnt = 0;

    for(int j = 1; j <= 6; j++)
    {

       // Number should not have a
       // leading zero and it
       // should be a prime number
       if (i - j >= 0 &&
           number[i - j] != '0' &&
           isPrime(number.Substring(i - j, j)))
       {
           cnt += rec(number, i - j, dp);
           cnt %= MOD;
       }
    }
    return dp[i] = cnt;
}

// Function to count the
// number of prime Strings
static int countPrimeStrings(String number)
{
    int n = number.Length;
    int []dp = new int[n + 1];

    for(int j = 0; j < dp.Length; j++)
       dp[j] = -1;
    dp[0] = 1;

    return rec(number, n, dp);
}

// Driver code
public static void Main(String[] args)
{
    buildSieve();

    String s1 = "3175";

    Console.Write(countPrimeStrings(s1) + "\n");
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript implementation to count total
// number of ways to split a String
// to get prime numbers
let MOD = 1000000007;
let sieve = new Array(1000000);

// Function to build sieve
function buildSieve()
{
    for(let i = 0; i < sieve.length; i++)
    {
        sieve[i] = true;
    }

    sieve[0] = false;
    sieve[1] = false;

    for(let p = 2; p * p <= 1000000; p++)
    {

       // If p is a prime
       if (sieve[p] == true)
       {

           // Update all multiples
           // of p as non prime
           for(let i = p * p; i < 1000000;
                   i += p)
              sieve[i] = false;
       }
    }
}

// Function to check whether a number
// is a prime number or not
function isPrime(number)
{
    let num = parseInt(number);
    return sieve[num];
}

// Function to find the count
// of ways to split String
// into prime numbers
function rec(number,i,dp)
{
    if (dp[i] != -1)
        return dp[i];
    let cnt = 0;

    for(let j = 1; j <= 6; j++)
    {

       // Number should not have a
       // leading zero and it
       // should be a prime number
       if (i - j >= 0 &&
           number[i - j] != '0' &&
           isPrime(number.substring(i - j, i)))
       {
           cnt += rec(number, i - j, dp);
           cnt %= MOD;
       }
    }
    return dp[i] = cnt;
}

// Function to count the
// number of prime Strings
function countPrimeStrings(number)
{
    let n = number.length;
    let dp = new Array(n + 1);

    for(let i = 0; i < (n + 1); i++)
    {
        dp[i] = -1;
    }

    dp[0] = 1;

    return rec(number, n, dp);
}

// Driver code
buildSieve();
let s1 = "3175";
document.write(countPrimeStrings(s1) + "<br>");

// This code is contributed by rag2127
</script>
```

**Output:** 

```
3
```

**时间复杂度:***O(N+N * log(log(N)))*
T5】辅助空间: *O(N)*