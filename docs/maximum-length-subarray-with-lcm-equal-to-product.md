# LCM 等于乘积的最大长度子阵列

> 原文:[https://www . geesforgeks . org/最大长度-subarray-with-LCM-等于乘积/](https://www.geeksforgeeks.org/maximum-length-subarray-with-lcm-equal-to-product/)

给定一个 **arr[]** ，任务是找到子阵列的最大长度，使得子阵列的 [LCM](https://www.geeksforgeeks.org/lcm-of-given-array-elements/) 等于子阵列中数字的乘积。如果不存在有效的子阵列，则打印 **-1** 。

**注意:**子阵列的长度必须≥ 2。

**示例:**

> **输入:** arr[] = { 6，10，21}
> **输出:** 2
> 子阵列{ 10，21}满足条件。
> 
> **输入:** arr[] = { 2，2，4}
> **输出:** -1
> 无子阵满足条件。因此，输出为-1。

**天真方法:**运行嵌套循环，检查长度≥ 2 的每个可能子数组的条件。如果子阵列满足条件，则更新 **ans = max(ans，长度(子阵列))**。最终打印出 **ans** 。

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

#define ll long long

// Function to calculate gcd(a, b)
int gcd(int a, int b)
{
    if (b == 0)
        return a;
    return gcd(b, a % b);
}

// Function to return max length of subarray
// that satisfies the condition
int maxLengthSubArray(const int* arr, int n)
{
    int maxLen = -1;
    for (int i = 0; i < n - 1; i++) {
        for (int j = i + 1; j < n; j++) {
            ll lcm = 1LL * arr[i];
            ll product = 1LL * arr[i];

            // Update LCM and product of the
            // sub-array
            for (int k = i + 1; k <= j; k++) {
                lcm = (((arr[k] * lcm)) /
                          (gcd(arr[k], lcm)));
                product = product * arr[k];
            }

            // If the current sub-array satisfies
            // the condition
            if (lcm == product) {

                // Choose the maximum
                maxLen = max(maxLen, j - i + 1);
            }
        }
    }

    return maxLen;
}

// Driver code
int main()
{
    int arr[] = { 6, 10, 21 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << maxLengthSubArray(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;

class GFG
{

// Function to calculate gcd(a, b)
static int gcd(int a, int b)
{
    if (b == 0)
        return a;
    return gcd(b, a % b);
}

// Function to return max length of subarray
// that satisfies the condition
static int maxLengthSubArray(int arr[], int n)
{
    int maxLen = -1;
    for (int i = 0; i < n - 1; i++)
    {
        for (int j = i + 1; j < n; j++)
        {
            int lcm = 1 * arr[i];
            int product = 1 * arr[i];

            // Update LCM and product of the
            // sub-array
            for (int k = i + 1; k <= j; k++)

            {
                lcm = (((arr[k] * lcm)) /
                        (gcd(arr[k], lcm)));
                product = product * arr[k];
            }

            // If the current sub-array satisfies
            // the condition
            if (lcm == product)
            {

                // Choose the maximum
                maxLen = Math.max(maxLen, j - i + 1);
            }
        }
    }
    return maxLen;
}

// Driver code
public static void main(String args[])
{
    int arr[] = { 6, 10, 21 };
    int n = arr.length;
    System.out.println(maxLengthSubArray(arr, n));
}
}

// This code is contributed by
// Shashank_Sharma
```

## 蟒蛇 3

```
# Python3 implementation of the
# above approach

# Function to calculate gcd(a, b)
def gcd(a, b):
    if (b == 0):
        return a
    return gcd(b, a % b)

# Function to return max length of
# subarray that satisfies the condition
def maxLengthSubArray(arr, n):

    maxLen = -1
    for i in range(n - 1):
        for j in range(n):
            lcm = arr[i]
            product = arr[i]

            # Update LCM and product of the
            # sub-array
            for k in range(i + 1, j + 1):
                lcm = (((arr[k] * lcm)) //
                    (gcd(arr[k], lcm)))
                product = product * arr[k]

            # If the current sub-array satisfies
            # the condition
            if (lcm == product):

                # Choose the maximum
                maxLen = max(maxLen, j - i + 1)
    return maxLen

# Driver code
arr = [6, 10, 21 ]
n = len(arr)
print(maxLengthSubArray(arr, n))

# This code is contributed by
# mohit kumar 29
```

## C#

```
// C# implementation of the above approach
using System;

class GFG
{

// Function to calculate gcd(a, b)
static int gcd(int a, int b)
{
    if (b == 0)
        return a;
    return gcd(b, a % b);
}

// Function to return max length of subarray
// that satisfies the condition
static int maxLengthSubArray(int[] arr, int n)
{
    int maxLen = -1;
    for (int i = 0; i < n - 1; i++)
    {
        for (int j = i + 1; j < n; j++)
        {
            int lcm = 1 * arr[i];
            int product = 1 * arr[i];

            // Update LCM and product of the
            // sub-array
            for (int k = i + 1; k <= j; k++)

            {
                lcm = (((arr[k] * lcm)) /
                        (gcd(arr[k], lcm)));
                product = product * arr[k];
            }

            // If the current sub-array satisfies
            // the condition
            if (lcm == product)
            {

                // Choose the maximum
                maxLen = Math.Max(maxLen, j - i + 1);
            }
        }
    }
    return maxLen;
}

// Driver code
public static void Main()
{
    int[] arr = { 6, 10, 21 };
    int n = arr.Length;
    Console.Write(maxLengthSubArray(arr, n));
}
}

// This code is contributed by ita_c
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above approach

// Function to calculate gcd(a, b)
function gcd($a, $b)
{
    if ($b == 0)
        return $a;
    return gcd($b, $a % $b);
}

// Function to return max length of subarray
// that satisfies the condition
function maxLengthSubArray(&$arr, $n)
{
    $maxLen = -1;
    for ($i = 0; $i < $n - 1; $i++)
    {
        for ($j = $i + 1; $j < $n; $j++)
        {
            $lcm = $arr[$i];
            $product = $arr[$i];

            // Update LCM and product of the
            // sub-array
            for ($k = $i + 1; $k <= $j; $k++)
            {
                $lcm = ((($arr[$k] * $lcm)) /
                        (gcd($arr[$k], $lcm)));
                $product = $product * $arr[$k];
            }

            // If the current sub-array satisfies
            // the condition
            if ($lcm == $product)
            {

                // Choose the maximum
                $maxLen = max($maxLen, $j - $i + 1);
            }
        }
    }

    return $maxLen;
}

// Driver code
$arr = array(6, 10, 21 );
$n = sizeof($arr);
echo(maxLengthSubArray($arr, $n));

// This code is contributed by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>
// Javascript implementation of the above approach

// Function to calculate gcd(a, b)
function  gcd(a,b)
{
    if (b == 0)
        return a;
    return gcd(b, a % b);
}

// Function to return max length of subarray
// that satisfies the condition
function maxLengthSubArray(arr,n)
{
    let maxLen = -1;
    for (let i = 0; i < n - 1; i++)
    {
        for (let j = i + 1; j < n; j++)
        {
            let lcm = 1 * arr[i];
            let product = 1 * arr[i];

            // Update LCM and product of the
            // sub-array
            for (let k = i + 1; k <= j; k++)

            {
                lcm = (((arr[k] * lcm)) /
                        (gcd(arr[k], lcm)));
                product = product * arr[k];
            }

            // If the current sub-array satisfies
            // the condition
            if (lcm == product)
            {

                // Choose the maximum
                maxLen = Math.max(maxLen, j - i + 1);
            }
        }
    }
    return maxLen;
}

// Driver code
let arr=[6, 10, 21 ];
let n = arr.length;
document.write(maxLengthSubArray(arr, n));

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
2
```

**有效方法:**当子阵列中没有两个元素具有任何公共因子时，子阵列的 LCM 等于其乘积。

**例如:**

> arr[] = { 6，10，21 }
> **素因子分解得到:**
> arr[] = { 2 * 3，2 * 5，3 * 7 }
> 【6，10】有 2 作为公因数。
> 【6，10，21】有 2 作为 6 和 10 之间的公共因子。
> 子阵列[10，21]在任何 2 个元素之间没有公共因子。因此，答案= 2。

首先，对数字进行素分解来处理因子。为了计算其中没有 2 个元素具有共同因子的子阵列，我们使用[双指针技术。](https://www.geeksforgeeks.org/two-pointers-technique/)

两个指针从右边开始运行，它们代表当前的子数组。我们从右边开始在子数组中添加元素。现在有两种情况:

1.  如果一个元素与子数组中的当前元素没有共同的因子，则该元素被添加到当前子数组中。如果找到一个公共因子，那么从左边开始，元素随后被消除，直到新添加的元素没有找到公共因子。
2.  如果新添加的元素和现有元素之间没有共同因素，则更新 **ans = max(ans，子数组长度)**

下面是上述方法的实现:

## C++

```
// C++ implementation of the above approach
#include <bits/stdc++.h>

#define pb push_back
#define N 100005
#define MAX 1000002
#define mem(a, b) memset(a, b, sizeof(a))

using namespace std;

int prime[MAX];

// Stores array of primes for every element
vector<int> v[N];

// Stores the position of a prime in the subarray
// in two pointer technique
int f[MAX];

// Function to store smallest prime factor of numbers
void sieve()
{
    prime[0] = prime[1] = 1;
    for (int i = 2; i < MAX; i++) {
        if (!prime[i]) {
            for (int j = i * 2; j < MAX; j += i) {
                if (!prime[j])
                    prime[j] = i;
            }
        }
    }

    for (int i = 2; i < MAX; i++) {

        // If number is prime,
        // then smallest prime factor is the
        // number itself
        if (!prime[i])
            prime[i] = i;
    }
}

// Function to return maximum length of subarray
// with LCM = product
int maxLengthSubArray(int* arr, int n)
{
    // Initialize f with -1
    mem(f, -1);

    for (int i = 0; i < n; ++i) {

        // Prime factorization of numbers
        // Store primes in a vector for every element
        while (arr[i] > 1) {
            int p = prime[arr[i]];
            arr[i] /= p;
            v[i].pb(p);
        }
    }

    // Two pointers l and r
    // denoting left and right of subarray
    int l = 0, r = 1, ans = -1;

    // f is a mapping.
    // prime -> index in the current subarray
    // With the help of f,
    // we can detect whether a prime has
    // already occurred in the subarray
    for (int i : v[0]) {
        f[i] = 0;
    }

    while (l <= r && r < n) {
        int flag = 0;

        for (int i = 0; i < v[r].size(); i++) {

            // Map the prime to the index
            if (f[v[r][i]] == -1 || f[v[r][i]] == r) {
                f[v[r][i]] = r;
            }

            // If already occurred then,
            // start removing elements from the left
            else {
                flag = 1;
                break;
            }
        }

        // Remove elements if flag = 1
        if (flag) {

            // Nullify entries of element at index 'l'
            for (int i : v[l]) {
                f[i] = -1;
            }

            // Increment 'l'
            l++;
        }
        else {

            // Maximize the answer when
            // no common factor is found
            ans = max(ans, r - l + 1);
            r++;
        }
    }

    // One length subarray is discarded
    if (ans == 1)
        ans = -1;

    return ans;
}

// Driver code
int main()
{
    sieve();
    int arr[] = { 6, 10, 21 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << maxLengthSubArray(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.io.*;
import java.util.*;

class GFG{

static int N = 100005;
static int MAX = 1000002;
static int[] prime = new int[MAX];

// Stores array of primes for every element
static ArrayList<
       ArrayList<Integer>> v = new ArrayList<
                                   ArrayList<Integer>>();

// Stores the position of a prime in the
// subarray in two pointer technique
static int[] f = new int[MAX];

// Function to store smallest prime
// factor of numbers
static void sieve()
{
    for(int i = 0; i < N; i++)
    {
        v.add(new ArrayList<Integer>());
    }

    prime[0] = prime[1] = 1;

    for(int i = 2; i < MAX; i++)
    {
        if (prime[i] == 0)
        {
            for(int j = i * 2; j < MAX; j += i)
            {
                if (prime[j] == 0)
                {
                    prime[j] = i;
                }
            }
        }
    }

    for(int i = 2; i < MAX; i++)
    {

        // If number is prime, then
        // smallest prime factor is
        // the number itself
        if (prime[i] == 0)
        {
            prime[i] = i;
        }
    }
}

// Function to return maximum length of
// subarray with LCM = product
static int maxLengthSubArray(int[] arr, int n)
{

    // Initialize f with -1
    Arrays.fill(f, -1);

    for(int i = 0; i < n; ++i)
    {

        // Prime factorization of numbers
        // Store primes in a vector for
        // every element
        while (arr[i] > 1)
        {
            int p = prime[arr[i]];
            arr[i] /= p;
            v.get(i).add(p);
        }
    }

    // Two pointers l and r denoting
    // left and right of subarray
    int l = 0, r = 1, ans = -1;

    // f is a mapping.
    // prime -> index in the current subarray
    // With the help of f,
    // we can detect whether a prime has
    // already occurred in the subarray
    for(int i : v.get(0))
    {
        f[i] = 0;
    }

    while (l <= r && r < n)
    {
        int flag = 0;

        for(int i = 0; i < v.get(r).size(); i++)
        {

            // Map the prime to the index
            if (f[v.get(r).get(i)] == -1  ||
                f[v.get(r).get(i)] == r)
            {
                f[v.get(r).get(i)] = r;
            }

            // If already occurred then,
            // start removing elements
            // from the left
            else
            {
                flag = 1;
                break;
            }
        }

        // Remove elements if flag = 1
        if (flag != 0)
        {

            // Nullify entries of element
            // at index 'l'
            for(int i : v.get(l))
            {
                f[i] = -1;
            }

            // Increment 'l'
            l++;
        }
        else
        {

            // Maximize the answer when
            // no common factor is found
            ans = Math.max(ans, r - l + 1);
            r++;
        }

    }

    // One length subarray is discarded
    if (ans == 1)
    {
        ans = -1;
    }
    return ans;
}

// Driver code
public static void main(String[] args)
{
    sieve();
    int arr[] = { 6, 10, 21 };
    int n = arr.length;

    System.out.println(maxLengthSubArray(arr, n));
}
}

// This code is contributed by avanitrachhadiya2155
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

N = 100005
MAX = 1000002

prime = [0 for i in range(MAX + 1)]

# Stores array of primes for every element
v = [[] for i in range(N)]

# Stores the position of a prime in the subarray
# in two pointer technique
f = [-1 for i in range(MAX)]

# Function to store smallest prime factor of numbers
def sieve():

    prime[0], prime[1] = 1, 1

    for i in range(2, MAX + 1):
        if (prime[i] == 0):
            for j in range(i * 2, MAX, i):
                if (prime[j] == 0):
                    prime[j] = i

    for i in range(2, MAX):

        # If number is prime,
        # then smallest prime factor is the
        # number itself
        if (prime[i] == 0):
            prime[i] = i

# Function to return maximum length of subarray
# with LCM = product
def maxLengthSubArray(arr, n):

    # Initialize f with -1
    for i in range(n):
        f[i] = -1

    for i in range(n):

        # Prime factorization of numbers
        # Store primes in a vector for every element
        while (arr[i] > 1):
            p = prime[arr[i]]
            arr[i] //= p
            v[i].append(p)

    # Two pointers l and r
    # denoting left and right of subarray
    l, r, ans = 0, 1, -1

    # f is a mapping.
    # prime -> index in the current subarray
    # With the help of f,
    # we can detect whether a prime has
    # already occurred in the subarray
    for i in v[0]:
        f[i] = 0

    while (l <= r and r < n):
        flag = 0

        for i in range(len(v[r])):

            # Map the prime to the index
            if (f[v[r][i]] == -1 or f[v[r][i]] == r):
                f[v[r][i]] = r

            # If already occurred then,
            # start removing elements from the left
            else:
                flag = 1
                break

        # Remove elements if flag = 1
        if (flag):

            # Nullify entries of element at index 'l'
            for i in v[l]:
                f[i] = -1

            # Increment 'l'
            l += 1
        else :

            # Maximize the answer when
            # no common factor is found
            ans = max(ans, r - l + 1)
            r += 1

    # One length subarray is discarded
    if (ans == 1):
        ans = -1

    return ans

# Driver code
sieve()
arr = [6, 10, 21]
n = len(arr)
print(maxLengthSubArray(arr, n))

# This code is contributed by mohit kumar
```

## C#

```
// C# implementation of the above approach
using System;
using System.Collections.Generic;
class GFG
{

  static int N = 100005;
  static int MAX = 1000002;
  static int[] prime = new int[MAX];

  // Stores array of primes for every element
  static List<List<int>> v = new List<List<int>>();

  // Stores the position of a prime in the
  // subarray in two pointer technique
  static int[] f = new int[MAX];

  // Function to store smallest prime
  // factor of numbers
  static void sieve()
  {
    for(int i = 0; i < N; i++)
    {
      v.Add(new List<int>());
    }

    prime[0] = prime[1] = 1;

    for(int i = 2; i < MAX; i++)
    {
      if (prime[i] == 0)
      {
        for(int j = i * 2; j < MAX; j += i)
        {
          if (prime[j] == 0)
          {
            prime[j] = i;
          }
        }
      }
    }

    for(int i = 2; i < MAX; i++)
    {

      // If number is prime, then
      // smallest prime factor is
      // the number itself
      if (prime[i] == 0)
      {
        prime[i] = i;
      }
    }
  }

  // Function to return maximum length of
  // subarray with LCM = product
  static int maxLengthSubArray(int[] arr, int n)
  {
    // Initialize f with -1
    Array.Fill(f, -1);   
    for(int i = 0; i < n; ++i)
    {

      // Prime factorization of numbers
      // Store primes in a vector for
      // every element
      while (arr[i] > 1)
      {
        int p = prime[arr[i]];
        arr[i] /= p;
        v[i].Add(p);
      }
    }

    // Two pointers l and r denoting
    // left and right of subarray
    int l = 0, r = 1, ans = -1;

    // f is a mapping.
    // prime -> index in the current subarray
    // With the help of f,
    // we can detect whether a prime has
    // already occurred in the subarray

    foreach(int i in v[0])
    {
      f[i] = 0;
    }

    while (l <= r && r < n)
    {
      int flag = 0;        
      for(int i = 0; i < v[r].Count; i++)
      {

        // Map the prime to the index
        if (f[v[r][i]] == -1  ||
            f[v[r][i]] == r)
        {
          f[v[r][i]] = r;
        }

        // If already occurred then,
        // start removing elements
        // from the left
        else
        {
          flag = 1;
          break;
        }
      }

      // Remove elements if flag = 1
      if (flag != 0)
      {

        // Nullify entries of element
        // at index 'l'
        foreach(int i in v[l])
        {
          f[i] = -1;
        }

        // Increment 'l'
        l++;
      }
      else
      {

        // Maximize the answer when
        // no common factor is found
        ans = Math.Max(ans, r - l + 1);
        r++;
      }

    }

    // One length subarray is discarded
    if (ans == 1)
    {
      ans = -1;
    }
    return ans;
  }

  // Driver code
  static public void Main ()
  {
    sieve();
    int[] arr = { 6, 10, 21 };
    int n = arr.Length;
    Console.WriteLine(maxLengthSubArray(arr, n));
  }
}
// This code is contributed by rag2127
```

## java 描述语言

```
<script>
// Javascript implementation of the above approach

let N = 100005;
let MAX = 1000002;
let prime = new Array(MAX);
for(let i=0;i<prime.length;i++)
{
    prime[i]=0;
}
// Stores array of primes for every element
let v = [];

// Stores the position of a prime in the
// subarray in two pointer technique
let  f = new Array(MAX);

// Function to store smallest prime
// factor of numbers
function sieve()
{
    for(let i = 0; i < N; i++)
    {
        v.push([]);
    }

    prime[0] = prime[1] = 1;

    for(let i = 2; i < MAX; i++)
    {
        if (prime[i] == 0)
        {
            for(let j = i * 2; j < MAX; j += i)
            {
                if (prime[j] == 0)
                {
                    prime[j] = i;
                }
            }
        }
    }

    for(let i = 2; i < MAX; i++)
    {

        // If number is prime, then
        // smallest prime factor is
        // the number itself
        if (prime[i] == 0)
        {
            prime[i] = i;
        }
    }
}

// Function to return maximum length of
// subarray with LCM = product
function maxLengthSubArray(arr,n)
{
     // Initialize f with -1
    for(let i=0;i<f.length;i++)
    {
        f[i]=-1;
    }

    for(let i = 0; i < n; ++i)
    {

        // Prime factorization of numbers
        // Store primes in a vector for
        // every element
        while (arr[i] > 1)
        {
            let p = prime[arr[i]];
            arr[i] /= p;
            v[i].push(p);
        }
    }

    // Two pointers l and r denoting
    // left and right of subarray
    let l = 0, r = 1, ans = -1;

    // f is a mapping.
    // prime -> index in the current subarray
    // With the help of f,
    // we can detect whether a prime has
    // already occurred in the subarray
    for(let i=0;i< v[0].length;i++)
    {
        f[v[0][i]] = 0;
    }

    while (l <= r && r < n)
    {
        let flag = 0;

        for(let i = 0; i < v[r].length; i++)
        {

            // Map the prime to the index
            if (f[v[r][i]] == -1  ||
                f[v[r][i]] == r)
            {
                f[v[r][i]] = r;
            }

            // If already occurred then,
            // start removing elements
            // from the left
            else
            {
                flag = 1;
                break;
            }
        }

        // Remove elements if flag = 1
        if (flag != 0)
        {

            // Nullify entries of element
            // at index 'l'
            for(let i=0;i<v[l].length;i++)
            {
                f[v[l][i]] = -1;
            }

            // Increment 'l'
            l++;
        }
        else
        {

            // Maximize the answer when
            // no common factor is found
            ans = Math.max(ans, r - l + 1);
            r++;
        }

    }

    // One length subarray is discarded
    if (ans == 1)
    {
        ans = -1;
    }
    return ans;
}

// Driver code

sieve();
let arr=[ 6, 10, 21];
let n = arr.length;
document.write(maxLengthSubArray(arr, n));

// This code is contributed by patel2127
</script>
```

**Output:** 

```
2
```