# 用给定的 LCM 最小化 K 个正整数的和

> 原文:[https://www . geesforgeks . org/minimum-k 正整数之和-带给定-lcm/](https://www.geeksforgeeks.org/minimize-sum-of-k-positive-integers-with-given-lcm/)

给定两个正整数 **K** 和 **X** ，任务是找出具有 [LCM](https://www.geeksforgeeks.org/lcm-of-given-array-elements/) **X** 的 **K** 正整数(*允许的重复次数*)的最小可能和。

**示例:**

> **输入:** K = 2，X = 6
> **输出:** 5
> **说明:**
> K(= 2)个具有 LCM X(= 6)的最小可能和的正整数为{ 2，3 }。
> 因此，K(= 2)个正整数的最小可能和= (2 + 3) = 5。
> 因此，要求输出为 5。
> 
> **输入:** K = 3 X = 11
> **输出:** 13
> **说明:**
> K(= 3)个具有 LCM X(= 11)的最小可能和的正整数为{ 1，1，11 }。
> 因此，K(= 3)个正整数的最小可能和= (1 + 1 + 11) = 13。
> 因此，要求的输出是 13。

**方法:**使用[贪婪手法](https://www.geeksforgeeks.org/greedy-algorithms/)可以解决问题。这个想法是代表 **X** 以[主要力量](https://en.wikipedia.org/wiki/Prime_power)的产物的形式。以所有可能的方式从 **X** 的所有素数幂中选择 **K** 素数幂，并计算它们各自的和。最后，打印它们中最小可能的总和。按照以下步骤解决问题:

*   初始化一个[数组](https://www.geeksforgeeks.org/vector-in-cpp-stl/)，比如**素数[]** ，来存储 **X** 的所有[素数](https://en.wikipedia.org/wiki/Prime_power)。
*   如果数组**prime pow【】**的长度小于或等于 **K** ，则在 **K** 正整数中包含**prime pow【】**的所有数组元素，并且 **K** 正整数的剩余元素必须为 **1** 。最后打印 **K** 正整数之和

> **图解:**
> 如果 K = 5，X = 240
> primePow[] = { 2 <sup>4</sup> ，3 <sup>1</sup> ，5 <sup>1</sup> } = { 16，3，5 }
> K 个正整数将为{ 16，3，5，1，1 }
> 因此，K 个正整数之和将为 26

*   否则，以所有可能的方式将 **primePow[]** 数组划分为 **K** 组，并计算它们各自的和。最后，打印 **K** 正整数的最小和。

> 如果 K = 3，X = 210
> primePow[] = { 2 <sup>1</sup> ，3 <sup>1</sup> ，5 <sup>1</sup> ，5 <sup>1</sup> } = { 2，3，5，7 }
> 将 primePow[]数组划分为{ { 2，3 }，{ 5 }，{ 7 } }
> 210 =(2 * 3)*(5)* 7 = 6 * 5 * 7
> K 个正整数将为{ 6

下面是上述实现的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the prime
// power of X
vector<int> primePower(int X)
{

    // Stores prime powers of X
    vector<int> primePow;

    // Iterate over the range [2, sqrt(X)]
    for (int i = 2; i * i <= X; i++) {

        // If X is divisible by i
        if (X % i == 0) {

            // Stores prime power
            int p = 1;

            // Calculate prime power
            // of X
            while (X % i == 0) {

                // Update X
                X /= i;

                // Update p
                p *= i;
            }

            // Insert prime powers
            // into primePow[]
            primePow.push_back(p);
        }
    }

    // If X exceeds 1
    if (X > 1) {
        primePow.push_back(X);
    }

    return primePow;
}

// Function to calculate the
// sum of array elements
int getSum(vector<int>& ar)
{
    // Stores sum of
    // array elements
    int sum = 0;

    // Traverse the array
    for (int i : ar) {

        // Update sum
        sum += i;
    }

    return sum;
}

// Function to partition array into K groups such
// that sum of elements of the K groups is minimum
int getMinSum(int pos, vector<int>& arr,
              vector<int>& primePow)
{

    // If count of prime powers
    // is equal to pos
    if (pos == primePow.size()) {
        return getSum(arr);
    }

    // Stores minimum sum of of each
    // partition of arr[] into K groups
    int res = INT_MAX;

    // Traverse the array arr[]
    for (int i = 0; i < arr.size();
         i++) {

        // Include primePow[pos] into
        // i-th groups
        arr[i] *= primePow[pos];

        // Update res
        res = min(res, getMinSum(pos + 1,
                                 arr, primePow));

        // Remove factors[pos] from
        // i-th groups
        arr[i] /= primePow[pos];
    }

    return res;
}

// Utility function to calculate minimum sum
// of K positive integers whose LCM is X
int minimumSumWithGivenLCM(int k, int x)
{
    // Stores all prime powers of X
    vector<int> primePow = primePower(x);

    // Stores count of prime powers
    int n = primePow.size();

    // Stores minimum sum of K positive
    // integers whose LCM is X
    int sum = 0;

    // If n is less than
    // or equal to k
    if (n <= k) {

        // Traverse primePow[] array
        for (int i : primePow) {

            // Update sum
            sum += i;
        }

        // Update sum
        sum += k - n;
    }

    else {

        // arr[i]: Stores element in i-th group
        // by partitioning the primePow[] array
        vector<int> arr(k, 1);

        // Update sum
        sum = getMinSum(0, arr, primePow);
    }

    return sum;
}

// Driver Code
int main()
{
    int k = 3, x = 210;

    cout << minimumSumWithGivenLCM(k, x);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to find the prime
// power of X
static Vector<Integer> primePower(int X)
{

    // Stores prime powers of X
    Vector<Integer> primePow = new Vector<Integer>();

    // Iterate over the range [2, Math.sqrt(X)]
    for (int i = 2; i * i <= X; i++) {

        // If X is divisible by i
        if (X % i == 0) {

            // Stores prime power
            int p = 1;

            // Calculate prime power
            // of X
            while (X % i == 0) {

                // Update X
                X /= i;

                // Update p
                p *= i;
            }

            // Insert prime powers
            // into primePow[]
            primePow.add(p);
        }
    }

    // If X exceeds 1
    if (X > 1) {
        primePow.add(X);
    }

    return primePow;
}

// Function to calculate the
// sum of array elements
static int getSum(int []ar)
{
    // Stores sum of
    // array elements
    int sum = 0;

    // Traverse the array
    for (int i : ar) {

        // Update sum
        sum += i;
    }

    return sum;
}

// Function to partition array into K groups such
// that sum of elements of the K groups is minimum
static int getMinSum(int pos, int []arr,
              Vector<Integer> primePow)
{

    // If count of prime powers
    // is equal to pos
    if (pos == primePow.size()) {
        return getSum(arr);
    }

    // Stores minimum sum of of each
    // partition of arr[] into K groups
    int res = Integer.MAX_VALUE;

    // Traverse the array arr[]
    for (int i = 0; i < arr.length;
         i++) {

        // Include primePow[pos] into
        // i-th groups
        arr[i] *= primePow.get(pos);

        // Update res
        res = Math.min(res, getMinSum(pos + 1,
                                 arr, primePow));

        // Remove factors[pos] from
        // i-th groups
        arr[i] /= primePow.get(pos);
    }

    return res;
}

// Utility function to calculate minimum sum
// of K positive integers whose LCM is X
static int minimumSumWithGivenLCM(int k, int x)
{
    // Stores all prime powers of X
    Vector<Integer> primePow = primePower(x);

    // Stores count of prime powers
    int n = primePow.size();

    // Stores minimum sum of K positive
    // integers whose LCM is X
    int sum = 0;

    // If n is less than
    // or equal to k
    if (n <= k) {

        // Traverse primePow[] array
        for (int i : primePow) {

            // Update sum
            sum += i;
        }

        // Update sum
        sum += k - n;
    }

    else {

        // arr[i]: Stores element in i-th group
        // by partitioning the primePow[] array
        int []arr = new int[k];
        Arrays.fill(arr, 1);

        // Update sum
        sum = getMinSum(0, arr, primePow);
    }

    return sum;
}

// Driver Code
public static void main(String[] args)
{
    int k = 3, x = 210;

    System.out.print(minimumSumWithGivenLCM(k, x));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find the prime
# power of X
def primePower(X):

    # Stores prime powers of X
    primePow = []

    # Iterate over the range [2, sqrt(X)]
    for i in range(2, X + 1):

        if i * i > X + 1:
            break

        # If X is divisible by i
        if (X % i == 0):

            # Stores prime power
            p = 1

            # Calculate prime power
            # of X
            while (X % i == 0):

                # Update X
                X //= i

                # Update p
                p *= i

            # Insert prime powers
            # into primePow[]
            primePow.append(p)

    # If X exceeds 1
    if (X > 1):
        primePow.append(X)

    return primePow

# Function to calculate the
# sum of array elements
def getSum(ar):

    # Stores sum of
    # array elements
    sum = 0

    # Traverse the array
    for i in ar:

        # Update sum
        sum += i

    return sum

# Function to partition array into K groups such
# that sum of elements of the K groups is minimum
def getMinSum(pos, arr, primePow):

    # If count of prime powers
    # is equal to pos
    if (pos == len(primePow)):
        return getSum(arr)

    # Stores minimum sum of of each
    # partition of arr[] into K groups
    res = 10**9

    # Traverse the array arr[]
    for i in range(len(arr)):

        # Include primePow[pos] into
        # i-th groups
        arr[i] *= primePow[pos]

        # Update res
        res = min(res, getMinSum(pos + 1, arr, primePow))

        #Remove factors[pos] from
        #i-th groups
        arr[i] //= primePow[pos]

    return res

# Utility function to calculate minimum sum
# of K positive integers whose LCM is X
def minimumSumWithGivenLCM(k, x):

    # Stores all prime powers of X
    primePow = primePower(x)

    # Stores count of prime powers
    n = len(primePow)

    # Stores minimum sum of K positive
    # integers whose LCM is X
    sum = 0

    # If n is less than
    # or equal to k
    if (n <= k):

        # Traverse primePow[] array
        for i in primePow:

            # Update sum
            sum += i

        # Update sum
        sum += k - n
    else:

        # arr[i]: Stores element in i-th group
        # by partitioning the primePow[] array
        arr = [1] * (k)

        # Update sum
        sum = getMinSum(0, arr, primePow)

    return sum

# Driver Code
if __name__ == '__main__':
    k = 3
    x = 210

    print(minimumSumWithGivenLCM(k, x))

    # This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to find the prime
// power of X
static List<int> primePower(int X)
{

    // Stores prime powers of X
    List<int> primePow = new List<int>();

    // Iterate over the range [2, Math.Sqrt(X)]
    for(int i = 2; i * i <= X; i++)
    {

        // If X is divisible by i
        if (X % i == 0)
        {

            // Stores prime power
            int p = 1;

            // Calculate prime power
            // of X
            while (X % i == 0)
            {

                // Update X
                X /= i;

                // Update p
                p *= i;
            }

            // Insert prime powers
            // into primePow[]
            primePow.Add(p);
        }
    }

    // If X exceeds 1
    if (X > 1)
    {
        primePow.Add(X);
    }
    return primePow;
}

// Function to calculate the
// sum of array elements
static int getSum(int []ar)
{

    // Stores sum of
    // array elements
    int sum = 0;

    // Traverse the array
    foreach(int i in ar)
    {

        // Update sum
        sum += i;
    }
    return sum;
}

// Function to partition array into K groups such
// that sum of elements of the K groups is minimum
static int getMinSum(int pos, int []arr,
                List<int> primePow)
{

    // If count of prime powers
    // is equal to pos
    if (pos == primePow.Count)
    {
        return getSum(arr);
    }

    // Stores minimum sum of of each
    // partition of []arr into K groups
    int res = int.MaxValue;

    // Traverse the array []arr
    for(int i = 0; i < arr.Length; i++)
    {

        // Include primePow[pos] into
        // i-th groups
        arr[i] *= primePow[pos];

        // Update res
        res = Math.Min(res, getMinSum(
            pos + 1, arr, primePow));

        // Remove factors[pos] from
        // i-th groups
        arr[i] /= primePow[pos];
    }
    return res;
}

// Utility function to calculate minimum sum
// of K positive integers whose LCM is X
static int minimumSumWithGivenLCM(int k, int x)
{

    // Stores all prime powers of X
    List<int> primePow = primePower(x);

    // Stores count of prime powers
    int n = primePow.Count;

    // Stores minimum sum of K positive
    // integers whose LCM is X
    int sum = 0;

    // If n is less than
    // or equal to k
    if (n <= k)
    {

        // Traverse primePow[] array
        foreach(int i in primePow)
        {

            // Update sum
            sum += i;
        }

        // Update sum
        sum += k - n;
    }

    else
    {

        // arr[i]: Stores element in i-th group
        // by partitioning the primePow[] array
        int []arr = new int[k];
        for(int l = 0; l < arr.Length; l++)
            arr[l] = 1;

        // Update sum
        sum = getMinSum(0, arr, primePow);
    }
    return sum;
}

// Driver Code
public static void Main(String[] args)
{
    int k = 3, x = 210;

    Console.Write(minimumSumWithGivenLCM(k, x));
}
}

// This code is contributed by aashish1995
```

## java 描述语言

```
<script>

// JavaScript program to implement
// the above approach

// Function to find the prime
// power of X
function primePower(X)
{
    let primePow = [];
    // Iterate over the range [2, Math.sqrt(X)]
    for (let i = 2; i * i <= X; i++) {

        // If X is divisible by i
        if (X % i == 0) {

            // Stores prime power
            let p = 1;

            // Calculate prime power
            // of X
            while (X % i == 0) {

                // Update X
                X /= i;

                // Update p
                p *= i;
            }

            // Insert prime powers
            // into primePow[]
            primePow.push(p);
        }
    }

    // If X exceeds 1
    if (X > 1) {
        primePow.push(X);
    }

    return primePow;
}

// Function to calculate the
// sum of array elements
function getSum(ar)
{
    // Stores sum of
    // array elements
    let sum = 0;

    // Traverse the array
    for (let i=0;i< ar.length;i++) {

        // Update sum
        sum += ar[i];
    }

    return sum;
}

// Function to partition array into K groups such
// that sum of elements of the K groups is minimum
function getMinSum(pos,arr,primePow)
{
    // If count of prime powers
    // is equal to pos
    if (pos == primePow.length) {
        return getSum(arr);
    }

    // Stores minimum sum of of each
    // partition of arr[] into K groups
    let res = Number.MAX_VALUE;

    // Traverse the array arr[]
    for (let i = 0; i < arr.length;
         i++) {

        // Include primePow[pos] into
        // i-th groups
        arr[i] *= primePow[pos];

        // Update res
        res = Math.min(res, getMinSum(pos + 1,
                                 arr, primePow));

        // Remove factors[pos] from
        // i-th groups
        arr[i] /= primePow[pos];
    }

    return res;
}

// Utility function to calculate minimum sum
// of K positive integers whose LCM is X
function minimumSumWithGivenLCM(k,x)
{
    // Stores all prime powers of X
    let primePow = primePower(x);

    // Stores count of prime powers
    let n = primePow.length;

    // Stores minimum sum of K positive
    // integers whose LCM is X
    let sum = 0;

    // If n is less than
    // or equal to k
    if (n <= k) {

        // Traverse primePow[] array
        for (let i=0;i< primePow.length;i++) {

            // Update sum
            sum += primePow[i];
        }

        // Update sum
        sum += k - n;
    }

    else {

        // arr[i]: Stores element in i-th group
        // by partitioning the primePow[] array
        let arr = new Array(k);
        for(let i=0;i<k;i++)
        {
            arr[i]=1;
        }

        // Update sum
        sum = getMinSum(0, arr, primePow);
    }

    return sum;
}

// Driver Code
let k = 3, x = 210;

document.write(minimumSumWithGivenLCM(k, x));

// This code is contributed by patel2127

</script>
```

**Output:** 

```
18
```

***时间复杂度:** O(sqrt(X) + 3 <sup>Y</sup> ，其中 Y 为质因数最大计数*
***辅助空间:** O(K + Y)*