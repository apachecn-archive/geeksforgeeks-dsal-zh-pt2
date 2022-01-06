# 长度为质数的不相交子阵串联得到的最大子序列和

> 原文:[https://www . geeksforgeeks . org/最大子序列-通过串联-不相交-长度为-质数的子阵列获得的和/](https://www.geeksforgeeks.org/maximum-subsequence-sum-obtained-by-concatenating-disjoint-subarrays-whose-lengths-are-prime/)

给定一个大小为 **N、**的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是找到一个[子序列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)的最大和，该子序列由长度为[素数](https://www.geeksforgeeks.org/prime-numbers/)的不相交的[子数组](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)连接而成。

**示例:**

> **输入:** arr[] = {10，10，7，10，10，10}
> **输出:** 50
> **解释:**
> 通过串联以下两个子阵列得到最大和的子序列:
> 
> 1.  长度为 2 的{10，10}，是质数。
> 2.  长度为 3 的{10，10，10}，是质数。
> 
> 得到的子序列是{10，10，10，10，10}。
> 子序列之和为 50。
> 
> **输入:** arr[] = {11，8，12 }
> T3】输出: 31

**天真法:**最简单的方法是用[递归](https://www.geeksforgeeks.org/recursion/)计算子序列最大和的值。在每一步中，为每个小于 **N** 的[质数](https://www.geeksforgeeks.org/prime-numbers/)调用多次递归调用。递归关系由下式给出:

> sum(N)=(arr[N]+arr[N–1]+…arr[N–P+1])+sum(N–P–1)
> 其中，
> P 是所选子阵列的质数长度，
> sum(N)是找到结果子序列最大和的函数。

以上递推关系只针对一个[素数](https://www.geeksforgeeks.org/prime-numbers/)。因此，通过选择不同素数长度的不同子阵列，可以形成不止一个可能的子序列。下面是所形成的递归关系:

> sum(N) = max(sum(a <sub>N</sub> ，…，a<sub>N-P1+1</sub>)+sum(N–P1–1)，sum(a <sub>N</sub> ，…，a<sub>N-P2+1</sub>)+sum(N–P2–1)，…，sum(a <sub>N</sub> ，…，a<sub>N-Pk+1</sub>)+sum(N–P<sub>k</sub>–1

***时间复杂度:** O(K <sup>N</sup> )其中 K 是*的数*质数*小于 N 的数*近似 K = (N / LogN)*
***辅助空间:O** (1)*

[](https://www.geeksforgeeks.org/dynamic-programming/)****使用自下而上的方法:**上面的递归调用也可以使用辅助数组 **dp[]** 来减少，并计算[自下而上的方法](https://www.geeksforgeeks.org/difference-between-bottom-up-model-and-top-down-model/)中每个状态的值。以下是步骤:**

*   **创建一个辅助数组**质数[]** 来存储所有小于或等于 n 的质数**
*   **维护厄拉多塞的[筛，并遍历它以填充数组**质数【】**的值。](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)**
*   **创建一个大小为 **N** 的辅助数组 **dp[]** 。**
*   **将状态 **0** 和 **1** 初始化为 **dp[0] = 0** 和 **dp[1] = 0** 。**
*   **[在**【2，N】**范围内遍历阵](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **dp[]** ，并将各状态更新为:**

> **MSS(i) =最大[sum(a<sub>I</sub>…a<sub>I-P1+1</sub>)+sum(I-P1-1)，sum(a<sub>I</sub>…a<sub>I-P2+1</sub>)+sum(I-P2-1)，…sum(a<sub>I</sub>…a<sub>I-Pk+1</sub>)+sum(I-Pk-1)】对于所有质数 P1、P2、… Pk 小于 n**

*   **初始化 **pref[]** 数组存储[前缀和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)高效计算**和(l，…，r)** 。**

> **a<sub>I</sub>+a<sub>I+1</sub>+…a<sub>j</sub>= sum(I…j)= pref[j]–pref[I–1]**

*   **打印上述步骤后**DP【N】**的值作为结果。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;
#define MAX 100005

// Function to return all prime numbers
// smaller than N
vector<int> SieveOfEratosthenes()
{
    // Create a boolean array "prime[0..n]"
    bool seive[MAX];

    // Initialize all its entries as true
    memset(seive, true, sizeof(seive));

    for (int p = 2; p * p < MAX; p++) {

        // If prime[p] is not changed,
        // then it is a prime
        if (seive[p] == true) {

            // Update all multiples of
            // p greater than or equal
            // to the square of it
            for (int i = p * p;
                 i < MAX; i += p) {
                seive[i] = false;
            }
        }
    }

    // Stores all prime numbers
    // smaller than MAX
    vector<int> v;

    // Store all prime numbers
    for (int p = 2; p < MAX; p++) {

        // If p is prime
        if (seive[p]) {
            v.push_back(p);
        }
    }

    return v;
}

// Function to build the auxiliary DP
// array from the start
void build(int dp[], int arr[], int N)
{
    // Base Case
    dp[0] = 0;
    dp[1] = 0;

    // Stores all prime numbers < N
    vector<int> prime
        = SieveOfEratosthenes();

    // Stores prefix sum
    int pref[N + 1];
    pref[0] = 0;

    // Update prefix sum
    for (int i = 1; i <= N; i++) {
        pref[i] = pref[i - 1]
                  + arr[i - 1];
    }

    // Iterate over range
    for (int i = 2; i <= N; i++) {

        // Update each state i.e.. when
        // current element is excluded
        dp[i] = dp[i - 1];
        for (int j = 0;
             j <= prime.size(); j++) {

            // Find start & end index
            // of subarrays when prime[i]
            // is taken
            int r = i - 1;
            int l = r - prime[j] + 1;

            // Check if starting point
            // lies in the array
            if (l < 0)
                break;
            int temp = 0;

            // Include the elements
            // al al+1 ... ar
            temp = pref[r + 1] - pref[l];

            // Check if element lies before
            // start of selected subarray
            if (l - 2 >= 0)
                temp += dp[l - 2 + 1];

            // Update value of dp[i]
            dp[i] = max(dp[i], temp);
        }
    }
}

// Function to find the maximum sum
// subsequence with prime length
void maxSumSubseq(int arr[], int N)
{
    // Auxiliary DP array
    int dp[N + 1];

    // Build DP array
    build(dp, arr, N);

    // Print the result
    cout << dp[N];
}

// Driver Code
int main()
{
    // Given arr[]
    int arr[] = { 10, 10, 7, 10, 10, 10 };

    // Size of array
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    maxSumSubseq(arr, N);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.util.*;

class GFG{

static int MAX = 100005;

// Function to return all prime numbers
// smaller than N
static Vector<Integer> SieveOfEratosthenes()
{

    // Create a boolean array "prime[0..n]"
    boolean []seive = new boolean[MAX];

    // Initialize all its entries as true
    Arrays.fill(seive, true);

    for(int p = 2; p * p < MAX; p++)
    {

        // If prime[p] is not changed,
        // then it is a prime
        if (seive[p] == true)
        {

            // Update all multiples of
            // p greater than or equal
            // to the square of it
            for(int i = p * p; i < MAX; i += p)
            {
                seive[i] = false;
            }
        }
    }

    // Stores all prime numbers
    // smaller than MAX
    Vector<Integer> v = new Vector<Integer>();

    // Store all prime numbers
    for(int p = 2; p < MAX; p++)
    {

        // If p is prime
        if (seive[p])
        {
            v.add(p);
        }
    }
    return v;
}

// Function to build the auxiliary DP
// array from the start
static void build(int dp[], int arr[], int N)
{

    // Base Case
    dp[0] = 0;
    dp[1] = 0;

    // Stores all prime numbers < N
    Vector<Integer> prime = SieveOfEratosthenes();

    // Stores prefix sum
    int []pref = new int[N + 1];
    pref[0] = 0;

    // Update prefix sum
    for(int i = 1; i <= N; i++)
    {
        pref[i] = pref[i - 1] + arr[i - 1];
    }

    // Iterate over range
    for(int i = 2; i <= N; i++)
    {

        // Update each state i.e.. when
        // current element is excluded
        dp[i] = dp[i - 1];
        for(int j = 0; j <= prime.size(); j++)
        {

            // Find start & end index
            // of subarrays when prime[i]
            // is taken
            int r = i - 1;
            int l = r - prime.get(j) + 1;

            // Check if starting point
            // lies in the array
            if (l < 0)
                break;

            int temp = 0;

            // Include the elements
            // al al+1 ... ar
            temp = pref[r + 1] - pref[l];

            // Check if element lies before
            // start of selected subarray
            if (l - 2 >= 0)
                temp += dp[l - 2 + 1];

            // Update value of dp[i]
            dp[i] = Math.max(dp[i], temp);
        }
    }
}

// Function to find the maximum sum
// subsequence with prime length
static void maxSumSubseq(int arr[], int N)
{

    // Auxiliary DP array
    int []dp = new int[N + 1];

    // Build DP array
    build(dp, arr, N);

    // Print the result
    System.out.print(dp[N]);
}

// Driver Code
public static void main(String args[])
{

    // Given arr[]
    int arr[] = { 10, 10, 7, 10, 10, 10 };

    // Size of array
    int N = arr.length;

    // Function Call
    maxSumSubseq(arr, N);
}
}

// This code is contributed by ipg2016107
```

## **蟒蛇 3**

```
# Python3 program for the above approach
MAX = 100005

# Function to return all prime numbers
# smaller than N
def SieveOfEratosthenes():

    # Create a boolean array "prime[0..n]"
    seive = [True for i in range(MAX)]

    # Initialize all its entries as true
    # memset(seive, true, sizeof(seive))
    for p in range(2, MAX):
        if p * p > MAX:
            break

        # If prime[p] is not changed,
        # then it is a prime
        if (seive[p] == True):

            # Update all multiples of
            # p greater than or equal
            # to the square of it
            for i in range(p * p, MAX, p):
                seive[i] = False

    # Stores all prime numbers
    # smaller than MAX
    v = []

    # Store all prime numbers
    for p in range(2, MAX):

        # If p is prime
        if (seive[p]):
            v.append(p)

    return v

# Function to build the auxiliary DP
# array from the start
def build(dp, arr, N):

    # Base Case
    dp[0] = 0
    dp[1] = 0

    # Stores all prime numbers < N
    prime = SieveOfEratosthenes()

    # Stores prefix sum
    pref = [0 for i in range(N + 1)]
    pref[0] = 0

    # Update prefix sum
    for i in range(1, N + 1):
        pref[i] = pref[i - 1] + arr[i - 1]

    # Iterate over range
    for i in range(2, N + 1):

        # Update each state i.e.. when
        # current element is excluded
        dp[i] = dp[i - 1]

        for j in range(len(prime) + 1):

            # Find start & end index
            # of subarrays when prime[i]
            # is taken
            r = i - 1
            l = r - prime[j] + 1

            # Check if starting point
            # lies in the array
            if (l < 0):
                break

            temp = 0

            # Include the elements
            # al al+1 ... ar
            temp = pref[r + 1] - pref[l]

            # Check if element lies before
            # start of selected subarray
            if (l - 2 >= 0):
                temp += dp[l - 2 + 1]

            # Update value of dp[i]
            dp[i] = max(dp[i], temp)

# Function to find the maximum sum
# subsequence with prime length
def maxSumSubseq(arr, N):

    # Auxiliary DP array
    dp = [0 for i in range(N + 1)]

    # Build DP array
    build(dp, arr, N)

    # Print the result
    print(dp[N])

# Driver Code
if __name__ == '__main__':

    # Given arr[]
    arr = [ 10, 10, 7, 10, 10, 10 ]

    # Size of array
    N = len(arr)

    # Function Call
    maxSumSubseq(arr, N)

# This code is contributed by mohit kumar 29
```

## **C#**

```
// C# program for the
// above approach
using System;
using System.Collections.Generic;
class GFG{

static int MAX = 100005;

// Function to return all
// prime numbers smaller than N
static List<int> SieveOfEratosthenes()
{   
  // Create a bool array
  // "prime[0..n]"
  bool []seive = new bool[MAX];

  // Initialize all its entries
  // as true
  for(int i = 0; i < MAX; i++)
    seive[i] = true;

  for(int p = 2; p * p < MAX; p++)
  {
    // If prime[p] is not changed,
    // then it is a prime
    if (seive[p] == true)
    {
      // Update all multiples of
      // p greater than or equal
      // to the square of it
      for(int i = p * p;
              i < MAX; i += p)
      {
        seive[i] = false;
      }
    }
  }

  // Stores all prime numbers
  // smaller than MAX
  List<int> v = new List<int>();

  // Store all prime numbers
  for(int p = 2; p < MAX; p++)
  {
    // If p is prime
    if (seive[p])
    {
      v.Add(p);
    }
  }
  return v;
}

// Function to build the auxiliary
// DP array from the start
static void build(int []dp,
                  int []arr, int N)
{   
  // Base Case
  dp[0] = 0;
  dp[1] = 0;

  // Stores all prime
  // numbers < N
  List<int> prime =
            SieveOfEratosthenes();

  // Stores prefix sum
  int []pref = new int[N + 1];
  pref[0] = 0;

  // Update prefix sum
  for(int i = 1; i <= N; i++)
  {
    pref[i] = pref[i - 1] +
              arr[i - 1];
  }

  // Iterate over range
  for(int i = 2; i <= N; i++)
  {
    // Update each state i.e..
    // when current element
    // is excluded
    dp[i] = dp[i - 1];
    for(int j = 0;
            j <= prime.Count; j++)
    {
      // Find start & end index
      // of subarrays when prime[i]
      // is taken
      int r = i - 1;
      int l = r - prime[j] + 1;

      // Check if starting point
      // lies in the array
      if (l < 0)
        break;

      int temp = 0;

      // Include the elements
      // al al+1 ... ar
      temp = pref[r + 1] - pref[l];

      // Check if element lies
      // before start of selected
      // subarray
      if (l - 2 >= 0)
        temp += dp[l - 2 + 1];

      // Update value of dp[i]
      dp[i] = Math.Max(dp[i],
                       temp);
    }
  }
}

// Function to find the maximum
// sum subsequence with prime
// length
static void maxSumSubseq(int []arr,
                         int N)
{
  // Auxiliary DP array
  int []dp = new int[N + 1];

  // Build DP array
  build(dp, arr, N);

  // Print the result
  Console.Write(dp[N]);
}

// Driver Code
public static void Main(String []args)
{
  // Given []arr
  int []arr = {10, 10, 7,
               10, 10, 10};

  // Size of array
  int N = arr.Length;

  // Function Call
  maxSumSubseq(arr, N);
}
}

// This code is contributed by shikhasingrajput
```

## **java 描述语言**

```
<script>

// Javascript program for the above approach

let MAX = 100005

// Function to return all prime numbers
// smaller than N
function SieveOfEratosthenes()
{
    // Create a boolean array "prime[0..n]"
    let seive = new Array(MAX);

    // Initialize all its entries as true
    seive.fill(true)

    for (let p = 2; p * p < MAX; p++) {

        // If prime[p] is not changed,
        // then it is a prime
        if (seive[p] == true) {

            // Update all multiples of
            // p greater than or equal
            // to the square of it
            for (let i = p * p;
                 i < MAX; i += p) {
                seive[i] = false;
            }
        }
    }

    // Stores all prime numbers
    // smaller than MAX
    let v = new Array();

    // Store all prime numbers
    for (let p = 2; p < MAX; p++) {

        // If p is prime
        if (seive[p]) {
            v.push(p);
        }
    }

    return v;
}

// Function to build the auxiliary DP
// array from the start
function build(dp, arr, N)
{
    // Base Case
    dp[0] = 0;
    dp[1] = 0;

    // Stores all prime numbers < N
    let prime = SieveOfEratosthenes();

    // Stores prefix sum
    let pref = new Array(N + 1);
    pref[0] = 0;

    // Update prefix sum
    for (let i = 1; i <= N; i++) {
        pref[i] = pref[i - 1]
                  + arr[i - 1];
    }

    // Iterate over range
    for (let i = 2; i <= N; i++) {

        // Update each state i.e.. when
        // current element is excluded
        dp[i] = dp[i - 1];
        for (let j = 0;
             j <= prime.length; j++) {

            // Find start & end index
            // of subarrays when prime[i]
            // is taken
            let r = i - 1;
            let l = r - prime[j] + 1;

            // Check if starting point
            // lies in the array
            if (l < 0)
                break;
            let temp = 0;

            // Include the elements
            // al al+1 ... ar
            temp = pref[r + 1] - pref[l];

            // Check if element lies before
            // start of selected subarray
            if (l - 2 >= 0)
                temp += dp[l - 2 + 1];

            // Update value of dp[i]
            dp[i] = Math.max(dp[i], temp);
        }
    }
}

// Function to find the maximum sum
// subsequence with prime length
function maxSumSubseq(arr, N)
{
    // Auxiliary DP array
    let dp = new Array(N + 1);

    // Build DP array
    build(dp, arr, N);

    // Print the result
    document.write(dp[N]);
}

// Driver Code

    // Given arr[]
    let arr = [ 10, 10, 7, 10, 10, 10 ];

    // Size of array
    let N = arr.length;

    // Function Call
    maxSumSubseq(arr, N);

// This code is contributed by gfgking

</script>
```

****Output**

```
50
```** 

*****时间复杂度:** O(N * K)*
***辅助空间:** O(N)***