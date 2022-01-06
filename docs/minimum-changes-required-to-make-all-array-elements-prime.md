# 使所有数组元素成为质数所需的最小变化量

> 原文:[https://www . geesforgeks . org/minimum-changes-make-all-array-elements-prime/](https://www.geeksforgeeks.org/minimum-changes-required-to-make-all-array-elements-prime/)

给定一个整数数组 **arr[]** ，任务是计算将每个数组元素转换为其最近的素数所需的最小变化数。
**例:**

> **输入:** arr[] = {4，25，13，6，20}
> **输出:** 5
> **解释:**
> 
> *   将 4 转换为最接近的素数 5 需要 1 个增量。
> *   将 25 转换为最接近的素数 23 需要 2 次递减。
> *   13 本身就是质数。
> *   将 6 转换为最接近的素数 7 需要 1 个增量。
> *   将 20 转换为最接近的质数 19 需要 1 个减量。
> 
> 因此，所需的更改次数= 1 + 2 + 0 + 1 + 1 = 5
> 
> **输入:** arr[] = {1，2，9}
> **输出:** 3
> **解释:**
> 
> *   将 1 转换为最接近的素数 2 需要 1 个增量。
> *   2 本身就是质数。
> *   将 9 转换为最接近的素数 11 需要 2 个增量。
> 
> 因此，所需的更改次数= 1 + 0 + 2 = 3

**天真方法:**
遍历数组，对于每个数组元素，从 arr[i] + 1 开始找到其右边最近的素数，从 arr[I]–1 开始找到其左边最近的素数。一旦计算出来，从 arr[i]计算它们的差值，并考虑较小的差值。所有这些差异的总和给出了期望的输出。

***时间复杂度:** O(N * maxi <sup>2</sup> ，其中 maxi 表示数组中最大的元素。*

**高效途径:**
这个问题可以用厄拉多塞的[筛子解决。按照以下步骤解决问题:](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)

*   从给定数组中找到[最大元素](https://www.geeksforgeeks.org/how-to-find-the-maximum-element-of-a-vector-using-stl-in-c/)。
*   让**最大**成为数组中存在的最大元素。生成范围**【1，2 *最大】**内的所有质数并存储。
*   遍历数组，使用[下界](https://www.geeksforgeeks.org/upper_bound-and-lower_bound-for-vector-in-cpp-stl/)，比如 **x** ，为每个数组元素找到下一个更大质数的索引。
*   计算 arr[i]和素数[x]之间以及 arr[i]和素数[x–1]之间的绝对差。
*   将两者的最小值加到**和**上。
*   完成数组遍历后，打印**和**的最终值作为答案。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to generate all primes
vector<int> SieveOfEratosthenes(int n)
{
    bool prime[2 * n + 1];
    memset(prime, true, sizeof(prime));

    for (int p = 2; p * p <= 2 * n; p++) {

        // If p is a prime
        if (prime[p] == true) {

            // Mark all its multiples
            // as non-prime
            for (int i = p * p; i <= 2 * n;
                 i += p)
                prime[i] = false;
        }
    }

    vector<int> primes;

    // Store all prime numbers
    for (int p = 2; p <= 2 * n; p++)
        if (prime[p])
            primes.push_back(p);

    // Return the list of primes
    return primes;
}

// Function to calculate the
// minimum increments to
// convert every array elements
// to a prime
int minChanges(vector<int> arr)
{
    int n = arr.size();
    int ans = 0;

    // Extract maximum element
    // of the given array
    int maxi = *max_element(arr.begin(),
                            arr.end());

    vector<int> primes
        = SieveOfEratosthenes(maxi);

    for (int i = 0; i < n; i++) {

        // Extract the index which has
        // the next greater prime
        int x = lower_bound(primes.begin(),
                            primes.end(),
                            arr[i])
                - primes.begin();

        // Store the difference
        // between the prime and
        // the array element
        int minm = abs(primes[x]
                       - arr[i]);

        if (x > 1) {
            minm = min(minm,
                       abs(primes[x - 1]
                           - arr[i]));
        }

        ans += minm;
    }
    return ans;
}

// Driver Code
int main()
{

    vector<int> arr
        = { 4, 25, 13, 6, 20 };

    cout << minChanges(arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
import java.lang.*;

class GFG{

// Function to generate all primes
static ArrayList<Integer> SieveOfEratosthenes(int n)
{
    boolean[] prime = new boolean[2 * n + 1];
    Arrays.fill(prime, true);

    for(int p = 2; p * p <= 2 * n; p++)
    {

        // If p is a prime
        if (prime[p] == true)
        {

            // Mark all its multiples
            // as non-prime
            for(int i = p * p;
                    i <= 2 * n; i += p)
                prime[i] = false;
        }
    }

    ArrayList<Integer> primes = new ArrayList<>();

    // Store all prime numbers
    for(int p = 2; p <= 2 * n; p++)
        if (prime[p])
            primes.add(p);

    // Return the list of primes
    return primes;
}

// Function to calculate the
// minimum increments to
// convert every array elements
// to a prime
static int minChanges(int[] arr)
{
    int n = arr.length;
    int ans = 0;

    // Extract maximum element
    // of the given array
    int maxi = arr[0];
    for(int i = 1; i < arr.length; i++)
        maxi = Math.max(maxi, arr[i]);

    ArrayList<Integer> primes = SieveOfEratosthenes(maxi);

    for(int i = 0; i < n; i++)
    {

        // Extract the index which has
        // the next greater prime
        int x = -1;
        for(int j = 0; j < primes.size(); j++)
        {
            if (arr[i] == primes.get(j))
            {
                x = j;
                break;
            }
            else if (arr[i] < primes.get(j))
            {
                x = j;
                break;
            }
        }

        // Store the difference
        // between the prime and
        // the array element
        int minm = Math.abs(primes.get(x) - arr[i]);

        if (x > 1)
        {
            minm = Math.min(minm,
                            Math.abs(primes.get(x - 1) -
                                     arr[i]));
        }
        ans += minm;
    }
    return ans;
}

// Driver code
public static void main (String[] args)
{
    int[] arr = { 4, 25, 13, 6, 20 };

    System.out.println(minChanges(arr));
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python program to implement
# the above approach

# Function to generate all primes
def SieveOfEratosthenes(n):
    prime = [True for i in range(2 * n + 1)]
    p = 2
    while(p * p <= 2 * n):

        # If p is a prime
        if(prime[p] == True):

            # Mark all its multiples
            # as non-prime
            i = p * p
            while(i <= n * 2):
                prime[i] = False
                i += p
        p += 1
    primes = []

    # Store all prime numbers
    for p in range(2, (2 * n) + 1):
        if(prime[p]):
            primes.append(p)

    # Return the list of primes
    return primes

# Function to calculate the
# minimum increments to
# convert every array elements
# to a prime
def minChanges(arr):
    n = len(arr)
    ans = 0

    # Extract maximum element
    # of the given array
    maxi = max(arr)
    primes = SieveOfEratosthenes(maxi)
    for i in range(n):

        # Extract the index which has
        # the next greater prime
        x = -1
        for j in range(len(primes)):
            if(arr[i] == primes[j]):
                x = j
                break
            elif(arr[i] < primes[j]):
                x = j
                break

        # Store the difference
        # between the prime and
        # the array element
        minm = abs(primes[x] - arr[i])

        if(x > 1):
            minm = min(minm, abs(primes[x - 1]-arr[i]))
        ans += minm
    return ans

# Driver code
arr = [4, 25, 13, 6, 20]
print(minChanges(arr))

# This code is contributed by avanitrachhadiya2155
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections;
using System.Collections.Generic;
class GFG
{

// Function to generate all primes
static List<int> SieveOfEratosthenes(int n)
{
    bool[] prime = new bool[2 * n + 1];
    Array.Fill(prime, true);

    for(int p = 2; p * p <= 2 * n; p++)
    {

        // If p is a prime
        if (prime[p] == true)
        {

            // Mark all its multiples
            // as non-prime
            for(int i = p * p; i <= 2 * n; i += p)
                prime[i] = false;
        }
    }  
    List<int> primes = new List<int>();

    // Store all prime numbers
    for(int p = 2; p <= 2 * n; p++)
        if (prime[p])
            primes.Add(p);

    // Return the list of primes
    return primes;
}

// Function to calculate the
// minimum increments to
// convert every array elements
// to a prime
static int minChanges(int[] arr)
{
    int n = arr.Length;
    int ans = 0;

    // Extract maximum element
    // of the given array
    int maxi = arr[0];
    for(int i = 1; i < arr.Length; i++)
        maxi = Math.Max(maxi, arr[i]);       
    List<int> primes = SieveOfEratosthenes(maxi);
    for(int i = 0; i < n; i++)
    {

        // Extract the index which has
        // the next greater prime
        int x = -1;
        for(int j = 0; j < primes.Count; j++)
        {
            if (arr[i] == primes[j])
            {
                x = j;
                break;
            }
            else if (arr[i] < primes[j])
            {
                x = j;
                break;
            }
        }

        // Store the difference
        // between the prime and
        // the array element
        int minm = Math.Abs(primes[x]- arr[i]);

        if (x > 1)
        {
            minm = Math.Min(minm,
                            Math.Abs(primes[x - 1] -
                                     arr[i]));
        }
        ans += minm;
    }
    return ans;
}

// Driver code
public static void Main(string[] args)
{
    int[] arr = { 4, 25, 13, 6, 20 };

    Console.Write(minChanges(arr));
}
}

// This code is contributed by rutvik_56.
```

## java 描述语言

```
<script>
// Javascript Program to implement
// the above approach

// Function to generate all primes
function SieveOfEratosthenes(n)
{
    let prime  = new Array(2 * n + 1);
    prime.fill(true)

    for (let p = 2; p * p <= 2 * n; p++) {

        // If p is a prime
        if (prime[p] == true) {

            // Mark all its multiples
            // as non-prime
            for (let i = p * p; i <= 2 * n;
                i += p)
                prime[i] = false;
        }
    }

    let primes = new Array();

    // Store all prime numbers
    for (let p = 2; p <= 2 * n; p++)
        if (prime[p])
            primes.push(p);

    // Return the list of primes
    return primes;
}

// Function to calculate the
// minimum increments to
// convert every array elements
// to a prime
function minChanges(arr)
{
    let n = arr.length;
    let ans = 0;

    // Extract maximum element
    // of the given array
    let maxi = arr.sort((a, b) => b - a)[0];

    let primes
        = SieveOfEratosthenes(maxi);

    for (let i = 0; i < n; i++) {

        // Extract the index which has
        // the next greater prime

        let x = -1
        for(let j = 0; j < primes.length; j++){
            if(arr[i] == primes[j]){
                x = j
                break
            }
            else if(arr[i] < primes[j]){
                x = j
                break
            }
        }
        // Store the difference
        // between the prime and
        // the array element
        let minm = Math.abs(primes[x]
                    - arr[i]);

        if (x > 1) {
            minm = Math.min(minm,
                    Math.abs(primes[x - 1]
                        - arr[i]));
        }

        ans += minm;
    }
    return ans;
}

// Driver Code

    let arr = [ 4, 25, 13, 6, 20 ];

    document.write(minChanges(arr));

// This code is contributed by _saurabh_jaiswal
</script>
```

**Output:** 

```
5
```

***时间复杂度:**O(log(log(N))+O(NlogN)*
***辅助空间:** O(N)*