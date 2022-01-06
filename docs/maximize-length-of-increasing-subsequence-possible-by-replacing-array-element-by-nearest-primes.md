# 通过用最近的素数替换数组元素来最大化可能增加的子序列的长度

> 原文:[https://www . geeksforgeeks . org/通过用最近的素数替换数组元素来最大化递增子序列的长度/](https://www.geeksforgeeks.org/maximize-length-of-increasing-subsequence-possible-by-replacing-array-element-by-nearest-primes/)

给定一个数组 **arr[]，**，任务是通过将元素替换为更大或更小的[素数](https://www.geeksforgeeks.org/prime-numbers/)来最大化增加[子序列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的长度。

**示例:**

> **输入:** arr[] = {4，20，6，12}
> **输出:** 3
> **解释:**
> 将数组 arr[]修改为{3，19，5，11}以最大化答案，
> 其中{3，5，11}是长度为 3 的最长递增子序列。
> 
> **输入:** arr[] = {30，43，42，19}
> **输出:** 2
> **解释:**
> 将数组 arr[]修改为{31，43，42，19}以最大化答案，
> 其中{31，43}是长度为 2 的最长递增子序列。

**方法:**想法是用较小的质数和下一个质数替换每个元素，形成另一个序列，在这个序列上我们可以应用标准的[最长递增子序列](https://www.geeksforgeeks.org/longest-monotonically-increasing-subsequence-size-n-log-n/)算法。在较小的质数之前保留较大的质数保证了它们不能以任何递增的顺序同时存在。

下面是上述方法的实现:

## C++14

```
// C++ program for above approach
#include<bits/stdc++.h>
using namespace std;

// Function to check if a
// number is prime or not
bool isprime(int n)
{
    if (n < 2)
        return false;

    for(int i = 2; i * i <= n; i++)
        if (n % i == 0)
            return false;

    return true;
}

// Function to find nearest
// greater prime of given number
int nextprime(int n)
{
    while (!isprime(n))
        n++;

    return n;
}

// Function to find nearest
// smaller prime of given number
int prevprime(int n)
{
    if (n < 2)
        return 2;

    while (!isprime(n))
        n--;

    return n;
}

// Function to return length of longest
// possible increasing subsequence
int longestSequence(vector<int> A)
{

    // Length of given array
    int n = A.size();

    int M = 1;

    // Stores increasing subsequence
    vector<int> l;

    // Insert first element prevprime
    l.push_back(prevprime(A[0]));

    // Traverse over the array
    for(int i = 1; i < n; i++)
    {

        // Current element
        int x = A[i];

        // Check for contribution of
        // nextprime and prevprime
        // to the increasing subsequence
        // calculated so far
        for(int p :{ nextprime(x),
                     prevprime(x) })
        {
            int low = 0;
            int high = M - 1;

            // Reset first element of list,
            // if p is less or equal
            if (p <= l[0])
            {
                l[0] = p;
                continue;
            }

            // Finding appropriate position
            // of Current element in l
            while (low < high)
            {
                int mid = (low + high + 1) / 2;

                if (p > l[mid])
                    low = mid;
                else
                    high = mid - 1;
            }

            // Update the calculated position
            // with Current element
            if (low + 1 < M)
                l[low + 1] = p;

            // Otherwise add current element
            // in L and increase M
            // as list size increases
            else
            {
                l.push_back(p);
                M++;
            }
        }
    }

    // Return M as length of possible
    // longest increasing sequence
    return M;
}

// Driver Code
int main()
{
    vector<int> A = { 4, 20, 6, 12 };

    // Function call
    cout << (longestSequence(A));
}

// This code is contributed by mohit kumar 29
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program for above approach

import java.util.*;
import java.lang.*;

class GFG {

    // Function to check if a
    // number is prime or not
    static boolean isprime(int n)
    {
        if (n < 2)
            return false;

        for (int i = 2; i * i <= n; i++)
            if (n % i == 0)
                return false;

        return true;
    }

    // Function to find nearest
    // greater prime of given number
    static int nextprime(int n)
    {
        while (!isprime(n))
            n++;
        return n;
    }

    // Function to find nearest
    // smaller prime of given number
    static int prevprime(int n)
    {
        if (n < 2)
            return 2;

        while (!isprime(n))
            n--;

        return n;
    }

    // Function to return length of longest
    // possible increasing subsequence
    static int longestSequence(int[] A)
    {
        // Length of given array
        int n = A.length;

        int M = 1;

        // Stores increasing subsequence
        List<Integer> l
            = new ArrayList<>();

        // Insert first element prevprime
        l.add(prevprime(A[0]));

        // Traverse over the array
        for (int i = 1; i < n; i++) {
            // Current element
            int x = A[i];

            // Check for contribution of
            // nextprime and prevprime
            // to the increasing subsequence
            // calculated so far

            for (int p :
                 new int[] { nextprime(x),
                             prevprime(x) }) {

                int low = 0;
                int high = M - 1;

                // Reset first element of list,
                // if p is less or equal
                if (p <= l.get(0)) {
                    l.set(0, p);
                    continue;
                }

                // Finding appropriate position
                // of Current element in l
                while (low < high) {
                    int mid = (low + high + 1) / 2;

                    if (p > l.get(mid))
                        low = mid;
                    else
                        high = mid - 1;
                }

                // Update the calculated position
                // with Current element
                if (low + 1 < M)
                    l.set(low + 1, p);

                // Otherwise add current element
                // in L and increase M
                // as list size increases
                else {
                    l.add(p);
                    M++;
                }
            }
        }

        // Return M as length of possible
        // longest increasing sequence
        return M;
    }

    // Driver Code
    public static void main(String[] args)
    {

        int[] A = { 4, 20, 6, 12 };

        // Function call
        System.out.println(
            longestSequence(A));
    }
}
```

## 蟒蛇 3

```
# Python3 Program for
# the above approach

#Function to check if a
# number is prime or not
def isprime(n):

    if (n < 2):
        return False

    i = 2
    while i * i <= n:
        if (n % i == 0):
            return False
        i += 2

    return True

# Function to find nearest
# greater prime of given number
def nextprime(n):

    while (not isprime(n)):
        n += 1
    return n

# Function to find nearest
# smaller prime of given number
def prevprime(n):

    if (n < 2):
        return 2

    while (not isprime(n)):
        n -= 1

    return n

# Function to return length of longest
# possible increasing subsequence
def longestSequence(A):

    # Length of given array
    n = len(A)

    M = 1

    # Stores increasing subsequence
    l = []

    # Insert first element prevprime
    l.append(prevprime(A[0]))

    # Traverse over the array
    for i in range (1, n):

        # Current element
        x = A[i]

        # Check for contribution of
        # nextprime and prevprime
        # to the increasing subsequence
        # calculated so far
        for p in [nextprime(x), 
                  prevprime(x)]:
            low = 0
            high = M - 1

            # Reset first element of list,
            # if p is less or equal
            if (p <= l[0]):
                l[0] = p
                continue

            # Finding appropriate position
            # of Current element in l
            while (low < high) :
                mid = (low + high + 1) // 2

                if (p > l[mid]):
                    low = mid
                else:
                    high = mid - 1

            # Update the calculated position
            # with Current element
            if (low + 1 < M):
                l[low + 1] = p

            # Otherwise add current element
            # in L and increase M
            # as list size increases
            else :
                l.append(p)
                M += 1

    # Return M as length of possible
    # longest increasing sequence
    return M

# Driver Code
if __name__ == "__main__":

    A = [4, 20, 6, 12]

    # Function call
    print(longestSequence(A))

# This code is contributed by Chitranayal
```

## C#

```
// C# Program for
// the above approach
using System;
using System.Collections.Generic;
class GFG{

// Function to check if a
// number is prime or not
static bool isprime(int n)
{
  if (n < 2)
    return false;

  for (int i = 2; i * i <= n; i++)
    if (n % i == 0)
      return false;

  return true;
}

// Function to find nearest
// greater prime of given number
static int nextprime(int n)
{
  while (!isprime(n))
    n++;
  return n;
}

// Function to find nearest
// smaller prime of given number
static int prevprime(int n)
{
  if (n < 2)
    return 2;

  while (!isprime(n))
    n--;

  return n;
}

// Function to return length of longest
// possible increasing subsequence
static int longestSequence(int[] A)
{
  // Length of given array
  int n = A.Length;

  int M = 1;

  // Stores increasing
  // subsequence
  List<int> l = new List<int>();

  // Insert first element
  // prevprime
  l.Add(prevprime(A[0]));

  // Traverse over the array
  for (int i = 1; i < n; i++)
  {
    // Current element
    int x = A[i];

    // Check for contribution of
    // nextprime and prevprime
    // to the increasing subsequence
    // calculated so far
    foreach (int p in new int[] {nextprime(x),
                                 prevprime(x)})
    {
      int low = 0;
      int high = M - 1;

      // Reset first element
      // of list, if p is less
      // or equal
      if (p <= l[0])
      {
        l[0] =  p;
        continue;
      }

      // Finding appropriate position
      // of Current element in l
      while (low < high)
      {
        int mid = (low + high + 1) / 2;

        if (p > l[mid])
          low = mid;
        else
          high = mid - 1;
      }

      // Update the calculated position
      // with Current element
      if (low + 1 < M)
        l[low + 1] = p;

      // Otherwise add current element
      // in L and increase M
      // as list size increases
      else
      {
        l.Add(p);
        M++;
      }
    }
  }

  // Return M as length
  // of possible longest
  // increasing sequence
  return M;
}

// Driver Code
public static void Main(String[] args)
{
  int[] A = {4, 20, 6, 12};

  // Function call
  Console.WriteLine(longestSequence(A));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program for above approach

// Function to check if a
// number is prime or not
function isprime(n)
{
    if (n < 2)
        return false;

    for(let i = 2; i * i <= n; i++)
        if (n % i == 0)
            return false;

    return true;
}

// Function to find nearest
// greater prime of given number
function nextprime(n)
{
    while (!isprime(n))
        n++;

    return n;
}

// Function to find nearest
// smaller prime of given number
function prevprime(n)
{
    if (n < 2)
        return 2;

    while (!isprime(n))
        n--;

    return n;
}

// Function to return length of longest
// possible increasing subsequence
function longestSequence(A)
{

    // Length of given array
    let n = A.length;

    let M = 1;

    // Stores increasing subsequence
    let l = new Array();

    // Insert first element prevprime
    l.push(prevprime(A[0]));

    // Traverse over the array
    for(let i = 1; i < n; i++)
    {

        // Current element
        let x = A[i];

        // Check for contribution of
        // nextprime and prevprime
        // to the increasing subsequence
        // calculated so far
        for(let p of [nextprime(x), prevprime(x)])
        {
            let low = 0;
            let high = M - 1;

            // Reset first element of list,
            // if p is less or equal
            if (p <= l[0])
            {
                l[0] = p;
                continue;
            }

            // Finding appropriate position
            // of Current element in l
            while (low < high)
            {
                let mid = low + high + 1 / 2;

                if (p > l[mid])
                    low = mid;
                else
                    high = mid - 1;
            }

            // Update the calculated position
            // with Current element
            if (low + 1 < M)
                l[low + 1] = p;

            // Otherwise add current element
            // in L and increase M
            // as list size increases
            else
            {
                l.push(p);
                M++;
            }
        }
    }

    // Return M as length of possible
    // longest increasing sequence
    return M;
}

// Driver Code

let A = [ 4, 20, 6, 12 ];

// Function call
document.write(longestSequence(A));

// This code is contributed by gfgking

</script>
```

**Output:** 

```
3
```

**时间复杂度:***O(N×logN)*
T5】辅助空间: *O(N)*