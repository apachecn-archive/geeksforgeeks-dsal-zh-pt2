# 计数乘积模 10^9 + 7 等于 1 的对

> 原文:[https://www . geesforgeks . org/count-pairs-其乘积模 109-7 等于 1/](https://www.geeksforgeeks.org/count-pairs-whose-product-modulo-109-7-is-equal-to-1/)

给定一个[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是从给定数组中计算无序对 **(arr[i]，arr[j])** 的数量，使得**(arr[I]* arr[j])% 10<sup>9</sup>+7**等于 **1** 。

**示例:**

> **输入:** arr[] = {2，236426，280311812，50000004 }
> **输出:** 2
> **解释:**给定数组中的两个这样的对是:
> 
> 1.  (2 * 500000004) % 1000000007 = 1
> 2.  (236426 * 280311812) % 1000000007 = 1
> 
> **输入:** arr[] = {4434，923094278，6565 }
> T3】输出: 1

**天真方法:**解决问题最简单的方法是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)和[从给定数组](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)生成所有可能的对。对于每对，以 **10 <sup>9</sup> + 7** 为模计算它们的乘积。如果发现等于 **1** ，则增加该对的**计数**。最后打印最后得到的**计数**。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*

**高效方法:**要优化上述方法，使用以下属性:如果**(arr[I]* arr[j])% 1000000007 = 1**，那么 **arr[j]** 就是 **arr[i]** 在模 **10 <sup>9</sup> + 7** 下的[模逆](https://www.geeksforgeeks.org/multiplicative-inverse-under-modulo-m/)始终唯一。按照下面给出的步骤解决问题:

*   初始化一个[映射](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/) **散列**，以存储数组**arr【】**中每个元素的[频率。](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/)
*   初始化一个变量**配对计数**，以存储所需配对的计数。
*   [遍历数组](https://www.geeksforgeeks.org/iterating-arrays-java/)并计算 **modularInverse** ，其与**arr【I】**在 **10 <sup>9</sup> + 7** 下相反，如果发现 **modularInverse** 等于**hash【modularInverse】**将 **pairCount** 的计数减少 **1**
*   最后，打印 **pairCount / 2** 作为所需答案，因为通过上述方法，每对都已经被计数了两次。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;
#define MOD 1000000007

// Iterative Function to calculate (x^y) % MOD
long long int modPower(long long int x,
                       long long int y)
{
    // Initialize result
    long long int res = 1;

    // Update x if it exceeds MOD
    x = x % MOD;

    // If x is divisible by MOD
    if (x == 0)
        return 0;

    while (y > 0) {

        // If y is odd
        if (y & 1)

            // Multiply x with res
            res = (res * x) % MOD;

        // y must be even now
        y = y / 2;
        x = (x * x) % MOD;
    }
    return res;
}

// Function to count number of pairs
// whose product modulo 1000000007 is 1
int countPairs(long long int arr[], int N)
{
    // Stores the count of
    // desired pairs
    int pairCount = 0;

    // Stores the frequencies of
    // each array element
    map<long long int, int> hash;

    // Traverse the array and update
    // frequencies in hash
    for (int i = 0; i < N; i++) {

        hash[arr[i]]++;
    }

    for (int i = 0; i < N; i++) {

        // Calculate modular inverse of
        // arr[i] under modulo 1000000007
        long long int modularInverse
            = modPower(arr[i], MOD - 2);

        // Update desired count of pairs
        pairCount += hash[modularInverse];

        // If arr[i] and its modular inverse
        // is equal under modulo MOD
        if (arr[i] == modularInverse) {

            // Updating count of desired pairs
            pairCount--;
        }
    }

    // Return the final count
    return pairCount / 2;
}

int main()
{
    long long int arr[]
        = { 2, 236426, 280311812, 500000004 };
    int N = sizeof(arr) / sizeof(arr[0]);

    cout << countPairs(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

static final int MOD = 1000000007;

// Iterative Function to calculate (x^y) % MOD
static long modPower(long x, int y)
{

    // Initialize result
    long res = 1;

    // Update x if it exceeds MOD
    x = x % MOD;

    // If x is divisible by MOD
    if (x == 0)
        return 0;

    while (y > 0)
    {

        // If y is odd
        if (y % 2 == 1)

            // Multiply x with res
            res = (res * x) % MOD;

        // y must be even now
        y = y / 2;
        x = (x * x) % MOD;
    }
    return res;
}

// Function to count number of pairs
// whose product modulo 1000000007 is 1
static int countPairs(long arr[], int N)
{

    // Stores the count of
    // desired pairs
    int pairCount = 0;

    // Stores the frequencies of
    // each array element
    HashMap<Long, Integer> hash = new HashMap<>();

    // Traverse the array and update
    // frequencies in hash
    for(int i = 0; i < N; i++)
    {
        if (hash.containsKey(arr[i]))
        {
            hash.put(arr[i], hash.get(arr[i]) + 1);
        }
        else
        {
            hash.put(arr[i], 1);
        }
    }

    for(int i = 0; i < N; i++)
    {

        // Calculate modular inverse of
        // arr[i] under modulo 1000000007
        long modularInverse = modPower(arr[i],
                                       MOD - 2);

        // Update desired count of pairs
        if (hash.containsKey(modularInverse))
            pairCount += hash.get(modularInverse);

        // If arr[i] and its modular inverse
        // is equal under modulo MOD
        if (arr[i] == modularInverse)
        {

            // Updating count of desired pairs
            pairCount--;
        }
    }

    // Return the final count
    return pairCount / 2;
}

// Driver code
public static void main(String[] args)
{
    long arr[] = { 2, 236426, 280311812, 500000004 };
    int N = arr.length;

    System.out.print(countPairs(arr, N));
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
from collections import defaultdict
MOD = 1000000007

# Iterative Function to
# calculate (x^y) % MOD
def modPower(x, y):

    # Initialize result
    res = 1

    # Update x if it exceeds
    # MOD
    x = x % MOD

    # If x is divisible by
    # MOD
    if (x == 0):
        return 0

    while (y > 0):

        # If y is odd
        if (y & 1):

            # Multiply x with res
            res = (res * x) % MOD

        # y must be even now
        y = y // 2
        x = (x * x) % MOD

    return res

# Function to count number
# of pairs whose product
# modulo 1000000007 is 1
def countPairs(arr, N):

    # Stores the count of
    # desired pairs
    pairCount = 0

    # Stores the frequencies of
    # each array element
    hash1 = defaultdict(int)

    # Traverse the array and
    # update frequencies in hash
    for i in range(N):
        hash1[arr[i]] += 1

    for i in range(N):

        # Calculate modular inverse
        # of arr[i] under modulo
        # 1000000007
        modularInverse = modPower(arr[i],
                                  MOD - 2)

        # Update desired count of pairs
        pairCount += hash1[modularInverse]

        # If arr[i] and its modular
        # inverse is equal under
        # modulo MOD
        if (arr[i] == modularInverse):

            # Updating count of
            # desired pairs
            pairCount -= 1

    # Return the final count
    return pairCount // 2

# Driver code
if __name__ == "__main__":

    arr = [2, 236426,
           280311812,
           500000004]
    N = len(arr)
    print(countPairs(arr, N))

# This code is contributed by Chitranayal
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;

class GFG{

static int MOD = 1000000007;

// Iterative Function to calculate (x^y) % MOD
static long modPower(long x, int y)
{

    // Initialize result
    long res = 1;

    // Update x if it exceeds MOD
    x = x % MOD;

    // If x is divisible by MOD
    if (x == 0)
        return 0;

    while (y > 0)
    {

        // If y is odd
        if (y % 2 == 1)

            // Multiply x with res
            res = (res * x) % MOD;

        // y must be even now
        y = y / 2;
        x = (x * x) % MOD;
    }
    return res;
}

// Function to count number of pairs
// whose product modulo 1000000007 is 1
static int countPairs(long []arr, int N)
{

    // Stores the count of
    // desired pairs
    int pairCount = 0;

    // Stores the frequencies of
    // each array element
    Dictionary<long,
               int> hash = new Dictionary<long,
                                          int>();

    // Traverse the array and update
    // frequencies in hash
    for(int i = 0; i < N; i++)
    {
        if (hash.ContainsKey(arr[i]))
        {
            hash.Add(arr[i], hash[arr[i]] + 1);
        }
        else
        {
            hash.Add(arr[i], 1);
        }
    }

    for(int i = 0; i < N; i++)
    {

        // Calculate modular inverse of
        // arr[i] under modulo 1000000007
        long modularInverse = modPower(arr[i],
                                       MOD - 2);

        // Update desired count of pairs
        if (hash.ContainsKey(modularInverse))
            pairCount += hash[modularInverse];

        // If arr[i] and its modular inverse
        // is equal under modulo MOD
        if (arr[i] == modularInverse)
        {

            // Updating count of desired pairs
            pairCount--;
        }
    }

    // Return the final count
    return pairCount / 2;
}

// Driver code
public static void Main()
{
    long []arr = { 2, 236426, 280311812, 500000004 };
    int N = arr.Length;

    Console.WriteLine(countPairs(arr, N));
}
}

// This code is contributed by bgangwar59
```

**Output:** 

```
2
```

***时间复杂度:** O(NlogN)*
***辅助空间:** O(N)*