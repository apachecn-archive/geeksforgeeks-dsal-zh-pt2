# 将两个数的质因数相乘的最小次数

使两个数相等

> 原文:[https://www . geeksforgeeks . org/将两个数字乘以它们的质因数，得出相等的最小次数/](https://www.geeksforgeeks.org/make-two-numbers-equal-by-multiplying-with-their-prime-factors-minimum-number-of-times/)

给定两个数字 **X** 和 **Y** ，任务是通过重复乘以它们的[质因数](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)的最小次数来使两者相等。

**示例:**

> **输入:** X = 36，Y = 48
> **输出:** 3
> **说明:**
> 操作 1:选择 2(X 的质因数)与 X 相乘，现在 X = 72，Y = 48。
> 操作 2:选择 2(X 的质因数)与 X 相乘，现在，X = 144，Y = 48
> 操作 3:选择 3(Y 的质因数)与 X 相乘，现在，X = 144，Y = 144
> 
> **输入:** X = 10，Y = 14
> **输出:** -1

**方法:**思路是 **Y** 中存在 **X** 的每一个[素因子](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)，而 **Y** 的每一个[素因子](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)存在于 **X** 时，才能使 **X** 和 **Y** 相等。要计算使它们相等所需的最小操作数，请执行以下步骤:

*   计算 **X** 和 **Y** 的 [gcd](https://www.geeksforgeeks.org/stdgcd-c-inbuilt-function-finding-gcd/) ，说出 **GCD** ，找到 **newX = X / GCD** 和 **newY = Y / GCD** 去掉常用的[质因数](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)。
*   用**纽 X** 和**纽 Y** 的频率找到[质因数](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)。
*   检查 **newX** 的每个[质因数](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)是否存在于 **Y(** 将除 Y)中，以及 **newY** 的每个[质因数](https://www.geeksforgeeks.org/print-all-prime-factors-of-a-given-number/)是否存在于 **X(** 将除 X) **中。**如果不是**，**则返回 **-1。**
*   初始化一个变量，比如 **ans =0，**来存储所需的操作数。
*   [将 **newX** 和 **newY** 的所有素数的频率加到 **ans** 上。](https://www.geeksforgeeks.org/python-program-to-add-two-numbers/)
*   返回**和**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach 
#include <bits/stdc++.h>
using namespace std;

// Function to calculate total number of 
// prime factor with their prime factor 
unordered_map<int, int> PrimeFactor(int N)
{
    unordered_map<int, int> primef;

    // Iterate while the number is even 
    while (N % 2 == 0)
    {
        if (primef.count(2))
        {
            primef[2] += 1;
        }
        else 
        {
            primef[2] = 1;
        }

        // Reduce to half 
        N /= 2;
    }

    // Iterate up to sqrt(N) 
    for(int i = 3; i <= sqrt(N); i++) 
    {

        // Iterate while N has 
        // factors of i 
        while (N % i == 0) 
        {
            if (primef.count(i)) 
            {
                primef[i] += 1;
            }
            else 
            {
                primef[i] = 1;
            }

            // Removing one factor of i 
            N /= 2;
        }
    }
    if (N > 2)
    {
        primef[N] = 1;
    }
    return primef;
}

// Function to count the number of factors 
int CountToMakeEqual(int X, int Y)
{

    // Find the GCD 
    int gcdofXY = __gcd(X, Y);

    // Find multiples left in X and Y 
    int newX = Y / gcdofXY;
    int newY = X / gcdofXY;

    // Find prime factor of multiple 
    // left in X and Y 
    unordered_map<int, int> primeX;
    unordered_map<int, int> primeY;
    primeX = PrimeFactor(newX);
    primeY = PrimeFactor(newY);

    // Initialize ans 
    int ans = 0;

    // Check if it possible 
    // to obtain X or not 
    for(auto c : primeX) 
    {
        if (X % c.first != 0) 
        {
            return -1;
        }
        ans += primeX[c.first];
    }

    // Check if it possible to 
    // obtain Y or not 
    for(auto c : primeY) 
    {
        if (Y % c.first != 0)
        {
            return -1;
        }
        ans += primeY[c.first];
    }

    // return main ans 
    return ans;
}

// Driver code
int main()
{

    // Given Input 
    int X = 36;
    int Y = 48;

    // Function Call 
    int ans = CountToMakeEqual(X, Y);
    cout << ans << endl;
    return 0;
}

// This code is contributed by adarshsinghk
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
public class Main
{

    static int gcd(int a, int b)
    {

        // Everything divides 0
        if (b == 0)
        {
            return a;
        }
        return gcd(b, a % b);
    }

    // Function to calculate total number of
    // prime factor with their prime factor
    static HashMap<Integer, Integer> PrimeFactor(int N)
    {
        HashMap<Integer, Integer> primef = new HashMap<Integer, Integer>();

        // Iterate while the number is even
        while (N % 2 == 0)
        {
            if (primef.containsKey(2))
            {
                primef.put(2, primef.get(2) + 1);
            }
            else
            {
                primef.put(2, 1);
            }

            // Reduce to half
            N = N / 2;
        }

        // Iterate up to sqrt(N)
        for(int i = 3; i <= Math.sqrt(N); i++)
        {

            // Iterate while N has
            // factors of i
            while (N % i == 0)
            {
                if (primef.containsKey(i))
                {
                    primef.put(i, primef.get(i) + 1);
                }
                else
                {
                    primef.put(i, 1);
                }

                // Removing one factor of i
                N = N / 2;
            }
        }
        if (N > 2)
        {
            primef.put(N, 1);
        }
        return primef;
    }

    // Function to count the number of factors
    static int CountToMakeEqual(int X, int Y)
    {

        // Find the GCD
        int gcdofXY = gcd(X, Y);

        // Find multiples left in X and Y
        int newX = Y / gcdofXY;
        int newY = X / gcdofXY;

        // Find prime factor of multiple
        // left in X and Y
        HashMap<Integer, Integer> primeX = PrimeFactor(newX);
        HashMap<Integer, Integer> primeY = PrimeFactor(newY);

        // Initialize ans
        int ans = 0;

        // Check if it possible
        // to obtain X or not
        for (Map.Entry keys : primeX.entrySet()) {
            if (X % (int)keys.getKey() != 0)
            {
                return -1;
            }
            ans += primeX.get(keys.getKey());
        }

        // Check if it possible to
        // obtain Y or not
        for (Map.Entry keys : primeY.entrySet()) {
            if (Y % (int)keys.getKey() != 0)
            {
                return -1;
            }
            ans += primeY.get(keys.getKey());
        }

        // Return main ans
        return ans;
    }

    public static void main(String[] args) {
        // Given Input
        int X = 36;
        int Y = 48;

        // Function Call
        int ans = CountToMakeEqual(X, Y);
        System.out.println(ans);
    }
}

// This code is contributed by mukesh07.
```

## 蟒蛇 3

```
# Python program for the above approach
import math

# Function to calculate total number of
# prime factor with their prime factor

def PrimeFactor(N):
    ANS = dict()

    # Iterate while the number is even
    while N % 2 == 0:
        if 2 in ANS:
            ANS[2] += 1
        else:
            ANS[2] = 1

        # Reduce to half
        N = N//2

    # Iterate up to sqrt(N)
    for i in range(3, int(math.sqrt(N))+1, 2):

        # Iterate while N has
        # factors of i
        while N % i == 0:
            if i in ANS:
                ANS[i] += 1
            else:
                ANS[i] = 1

            # Removing one factor of i
            N = N // i

    if 2 < N:
        ANS[N] = 1

    return ANS

# Function to count the number of factors
def CountToMakeEqual(X, Y):

    # Find the GCD
    GCD = math.gcd(X, Y)

    # Find multiples left in X and Y
    newY = X//GCD
    newX = Y//GCD

    # Find prime factor of multiple
    # left in X and Y
    primeX = PrimeFactor(newX)
    primeY = PrimeFactor(newY)

    # Initialize ans
    ans = 0

    # Check if it possible
    # to obtain X or not
    for factor in primeX:

        if X % factor != 0:
            return -1
        ans += primeX[factor]

    # Check if it possible to
    # obtain Y or not
    for factor in primeY:

        if Y % factor != 0:
            return -1
        ans += primeY[factor]

    # return main ans
    return ans

# Driver Code
if __name__ == "__main__":

    # Given Input
    X = 36
    Y = 48

    # Function Call
    ans = CountToMakeEqual(X, Y)
    print(ans)
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

static int gcd(int a, int b)
{

    // Everything divides 0
    if (b == 0)
    {
        return a;
    }
    return gcd(b, a % b);
}

// Function to calculate total number of
// prime factor with their prime factor
static Dictionary<int, int> PrimeFactor(int N)
{
    Dictionary<int, 
               int> primef = new Dictionary<int, 
                                            int>(); 

    // Iterate while the number is even
    while (N % 2 == 0)
    {
        if (primef.ContainsKey(2))
        {
            primef[2]++;
        }
        else
        {
            primef[2] = 1;
        }

        // Reduce to half
        N = N / 2;
    }

    // Iterate up to sqrt(N)
    for(int i = 3; i <= Math.Sqrt(N); i++)
    {

        // Iterate while N has
        // factors of i
        while (N % i == 0)
        {
            if (primef.ContainsKey(i))
            {
                primef[i]++;
            }
            else
            {
                primef[i] = 1;
            }

            // Removing one factor of i
            N = N / 2;
        }
    }
    if (N > 2)
    {
        primef[N] = 1;
    }
    return primef;
}

// Function to count the number of factors
static int CountToMakeEqual(int X, int Y)
{

    // Find the GCD
    int gcdofXY = gcd(X, Y);

    // Find multiples left in X and Y
    int newX = Y / gcdofXY;
    int newY = X / gcdofXY;

    // Find prime factor of multiple
    // left in X and Y
    Dictionary<int, int> primeX = PrimeFactor(newX);
    Dictionary<int, int> primeY = PrimeFactor(newY);

    // Initialize ans
    int ans = 0;

    // Check if it possible
    // to obtain X or not
    foreach(KeyValuePair<int, int> keys in primeX)
    {
        if (X % keys.Key != 0)
        {
            return -1;
        }
        ans += primeX[keys.Key];
    }

    // Check if it possible to
    // obtain Y or not
    foreach(KeyValuePair<int, int> keys in primeY)
    {
        if (Y % keys.Key != 0)
        {
            return -1;
        }
        ans += primeY[keys.Key];
    }

    // Return main ans
    return ans;
}

// Driver Code
static void Main() 
{

    // Given Input
    int X = 36;
    int Y = 48;

    // Function Call
    int ans = CountToMakeEqual(X, Y);
    Console.Write(ans);
}
}

// This code is contributed by rameshtravel07
```

## java 描述语言

```
<script>
    // Javascript program for the above approach

    function gcd(a, b){

      // Everything divides 0
      if(b == 0){
        return a;
      }

      return gcd(b, a % b);
    }

    // Function to calculate total number of
    // prime factor with their prime factor
    function PrimeFactor(N)
    {
        let primef = new Map();

        // Iterate while the number is even
        while (N % 2 == 0)
        {
            if (primef.has(2))
            {
                primef.set(2, primef.get(2) + 1);
            }
            else
            {
                primef.set(2, 1);
            }

            // Reduce to half
            N = parseInt(N / 2, 10);
        }

        // Iterate up to sqrt(N)
        for(let i = 3; i <= Math.sqrt(N); i++)
        {

            // Iterate while N has
            // factors of i
            while (N % i == 0)
            {
                if (primef.has(i))
                {
                    primef.set(i, primef.get(i) + 1);
                }
                else
                {
                    primef.set(i, 1);
                }

                // Removing one factor of i
                N = parseInt(N / 2, 10);
            }
        }
        if (N > 2)
        {
            primef[N] = 1;
        }
        return primef;
    }

    // Function to count the number of factors
    function CountToMakeEqual(X, Y)
    {

        // Find the GCD
        let gcdofXY = gcd(X, Y);

        // Find multiples left in X and Y
        let newX = parseInt(Y / gcdofXY, 10);
        let newY = parseInt(X / gcdofXY, 10);

        // Find prime factor of multiple
        // left in X and Y
        let primeX = PrimeFactor(newX);
        let primeY = PrimeFactor(newY);

        // Initialize ans
        let ans = 0;

        // Check if it possible
        // to obtain X or not
        primeX.forEach((values,keys)=>
        {
            if (X % keys != 0)
            {
                return -1;
            }
            ans += primeX.get(keys);
        })
        ans+=1;

        // Check if it possible to
        // obtain Y or not
        primeY.forEach((values,keys)=>
        {
            if (Y % keys != 0)
            {
                return -1;
            }
            ans += primeY.get(keys);
        })

        // return main ans
        return ans;
    }

    // Given Input
    let X = 36;
    let Y = 48;

    // Function Call
    let ans = CountToMakeEqual(X, Y);
    document.write(ans);

// This code is contributed by decode2207.
</script>
```

**Output:** 

```
3
```

***时间复杂度:** O(sqrt(max(X，Y)))*
***辅助空间:** O(1)*