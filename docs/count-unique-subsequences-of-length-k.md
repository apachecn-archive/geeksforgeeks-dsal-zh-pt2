# 计数长度为 K 的唯一子序列

> 原文:[https://www . geesforgeks . org/count-unique-sequence-of-length-k/](https://www.geeksforgeeks.org/count-unique-subsequences-of-length-k/)

给定一个由 N 个数字和一个整数 k 组成的数组，任务是打印长度为 k 的唯一子序列的数量

示例:

```
Input : a[] = {1, 2, 3, 4}, k = 3 
Output : 4\. 
Unique Subsequences are: 
{1, 2, 3}, {1, 2, 4}, {1, 3, 4}, {2, 3, 4}

Input: a[] = {1, 1, 1, 2, 2, 2 }, k = 3
Output : 4 
Unique Subsequences are 
{1, 1, 1}, {1, 1, 2}, {1, 2, 2}, {2, 2, 2} 
```

**方法:**有一个众所周知的公式，可以从 N 个唯一的对象中选择多少个固定长度 K 的子序列。但是这里的问题有几个不同之处。其中之一是子序列的顺序很重要，必须像原始序列一样保留。对于这样的问题，不可能有现成的组合数学公式，因为结果取决于原始数组的顺序。

主要思想是通过子序列的长度反复处理。在每个循环步骤中，从末尾移动到开头，并使用上一步骤中较短的唯一组合计数来计数唯一组合。更严格地说，在每一步 j 上，我们保留一个长度为 N 的数组，p 处的每个元素意味着在 I 处元素的右边有多少个长度为 j 的唯一子序列，包括 I 本身。

下面是上述方法的实现。

## C++

```
#include <bits/stdc++.h>
using namespace std;

// Function which returns the numbe of
// unique subsequences of length K
int solution(vector<int>& A, int k)
{
    // seiz of the vector
    // which does is constant
    const int N = A.size();

    // bases cases
    if (N < k || N < 1 || k < 1)
        return 0;
    if (N == k)
        return 1;

    // Prepare arrays for recursion
    vector<int> v1(N, 0);
    vector<int> v2(N, 0);
    vector<int> v3(N, 0);

    // initiate separately for k = 1
    // initiate the last element
    v2[N - 1] = 1;
    v3[A[N - 1] - 1] = 1;

    // initiate all other elements of k = 1
    for (int i = N - 2; i >= 0; i--) {

        // initialize the front element
        // to vector v2
        v2[i] = v2[i + 1];

        // if element v[a[i]-1] is 0
        // then increment it in vector v2
        if (v3[A[i] - 1] == 0) {
            v2[i]++;
            v3[A[i] - 1] = 1;
        }
    }

    // iterate for all possible values of K
    for (int j = 1; j < k; j++) {

        // fill the vectors with 0
        fill(v3.begin(), v3.end(), 0);

        // fill(v1.begin(), v1.end(), 0)
        // the last must be 0 as from last no unique
        // subarray can be formed
        v1[N - 1] = 0;

        // Iterate for all index from which unique
        // subsequences can be formed
        for (int i = N - 2; i >= 0; i--) {

            // add the number of subsequence formed
            // from the next index
            v1[i] = v1[i + 1];

            // start with combinations on the
            // next index
            v1[i] = v1[i] + v2[i + 1];

            // Remove the elements which have
            // already been counted
            v1[i] = v1[i] - v3[A[i] - 1];

            // Update the number used
            v3[A[i] - 1] = v2[i + 1];
        }

        // prepare the next iteration
        // by filling v2 in v1
        v2 = v1;
    }

    // last answer is stored in v2
    return v2[0];
}

// Function to push the vector into an array
// and print all the unique subarrays
void solve(int a[], int n, int k)
{
    vector<int> v;

    // fill the vector with a[]
    v.assign(a, a + n);

    // Function call to print the count
    // of unique subsequences of size K
    cout << solution(v, k);
}

// Driver Code
int main()
{
    int a[] = { 1, 2, 3, 4 };
    int n = sizeof(a) / sizeof(a[0]);
    int k = 3;
    solve(a, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
import java.util.*;

class GFG{

// Function which returns the numbe of
// unique subsequences of length K
static int solution(int[] A, int N, int k)
{

    // Bases cases
    if (N < k || N < 1 || k < 1)
        return 0;
    if (N == k)
        return 1;

    // Prepare arrays for recursion
    int[] v1 = new int[N];
    int[] v2 = new int[N];
    int[] v3 = new int[N];

    // Initiate separately for k = 1
    // initiate the last element
    v2[N - 1] = 1;
    v3[A[N - 1] - 1] = 1;

    // Initiate all other elements of k = 1
    for(int i = N - 2; i >= 0; i--)
    {

        // Initialize the front element
        // to vector v2
        v2[i] = v2[i + 1];

        // If element v[a[i]-1] is 0
        // then increment it in vector v2
        if (v3[A[i] - 1] == 0)
        {
            v2[i]++;
            v3[A[i] - 1] = 1;
        }
    }

    // Iterate for all possible values of K
    for(int j = 1; j < k; j++)
    {

        // Fill the vectors with 0
        Arrays.fill(v3, 0);

        // Fill(v1.begin(), v1.end(), 0)
        // the last must be 0 as from last
        // no unique subarray can be formed
        v1[N - 1] = 0;

        // Iterate for all index from which
        // unique subsequences can be formed
        for(int i = N - 2; i >= 0; i--)
        {

            // Add the number of subsequence
            // formed from the next index
            v1[i] = v1[i + 1];

            // Start with combinations on the
            // next index
            v1[i] = v1[i] + v2[i + 1];

            // Remove the elements which have
            // already been counted
            v1[i] = v1[i] - v3[A[i] - 1];

            // Update the number used
            v3[A[i] - 1] = v2[i + 1];
        }
    }

    // Last answer is stored in v2
    return v2[0];
}

// Driver Code
public static void main(String[] args)
{
    int a[] = { 1, 2, 3, 4 };
    int n = a.length;
    int k = 3;

    System.out.print(solution(a, n, k));
}
}

// This code is contributed by amal kumar choubey
```

## 蟒蛇 3

```
# Function which returns the numbe of
# unique subsequences of length K
def solution( A, k):

    # seiz of the vector
    # which does is constant
    N = len(A)

    # bases cases
    if (N < k or N < 1 or k < 1):
        return 0
    if (N == k):
        return 1

    # Prepare arrays for recursion
    v1 = [0]*(N)
    v2 = [0]*N
    v3 = [0]*N

    # initiate separately for k = 1
    # initiate the last element
    v2[N - 1] = 1
    v3[A[N - 1] - 1] = 1

    # initiate all other elements of k = 1
    for i in range(N - 2,-1,-1):

        # initialize the front element
        # to vector v2
        v2[i] = v2[i + 1]

        # if element v[a[i]-1] is 0
        # then increment it in vector v2
        if (v3[A[i] - 1] == 0):
            v2[i] += 1
            v3[A[i] - 1] = 1

    # iterate for all possible values of K
    for j in range( 1, k) :

        # fill the vectors with 0
        v3 = [0]*N

        # fill(v1.begin(), v1.end(), 0)
        # the last must be 0 as from last no unique
        # subarray can be formed
        v1[N - 1] = 0

        # Iterate for all index from which unique
        # subsequences can be formed
        for i in range( N - 2, -1, -1) :

            # add the number of subsequence formed
            # from the next index
            v1[i] = v1[i + 1]

            # start with combinations on the
            # next index
            v1[i] = v1[i] + v2[i + 1]

            # Remove the elements which have
            # already been counted
            v1[i] = v1[i] - v3[A[i] - 1]

            # Update the number used
            v3[A[i] - 1] = v2[i + 1]

        # prepare the next iteration
        # by filling v2 in v1
        for i in range(len(v1)):
            v2[i] = v1[i]

    # last answer is stored in v2
    return v2[0]

# Function to push the vector into an array
# and print all the unique subarrays
def solve(a, n, k):

    # fill the vector with a[]
    v = a

    # Function call to print the count
    # of unique subsequences of size K
    print( solution(v, k))

# Driver Code
if __name__ == "__main__":

    a = [ 1, 2, 3, 4 ]
    n = len(a)
    k = 3
    solve(a, n, k)

# This code is contributed by chitranayal
```

## C#

```
using System;
class GFG{

// Function which returns the numbe of
// unique subsequences of length K
static int solution(int[] A, int N, int k)
{

    // Bases cases
    if (N < k || N < 1 || k < 1)
        return 0;
    if (N == k)
        return 1;

    // Prepare arrays for recursion
    int[] v1 = new int[N];
    int[] v2 = new int[N];
    int[] v3 = new int[N];

    // Initiate separately for k = 1
    // initiate the last element
    v2[N - 1] = 1;
    v3[A[N - 1] - 1] = 1;

    // Initiate all other elements of k = 1
    for(int i = N - 2; i >= 0; i--)
    {

        // Initialize the front element
        // to vector v2
        v2[i] = v2[i + 1];

        // If element v[a[i]-1] is 0
        // then increment it in vector v2
        if (v3[A[i] - 1] == 0)
        {
            v2[i]++;
            v3[A[i] - 1] = 1;
        }
    }

    // Iterate for all possible values of K
    for(int j = 1; j < k; j++)
    {

        // Fill the vectors with 0
        for(int i = 0; i < v3.GetLength(0); i++)
            v3[i] = 0;

        // Fill(v1.begin(), v1.end(), 0)
        // the last must be 0 as from last
        // no unique subarray can be formed
        v1[N - 1] = 0;

        // Iterate for all index from which
        // unique subsequences can be formed
        for(int i = N - 2; i >= 0; i--)
        {

            // Add the number of subsequence
            // formed from the next index
            v1[i] = v1[i + 1];

            // Start with combinations on the
            // next index
            v1[i] = v1[i] + v2[i + 1];

            // Remove the elements which have
            // already been counted
            v1[i] = v1[i] - v3[A[i] - 1];

            // Update the number used
            v3[A[i] - 1] = v2[i + 1];
        }
    }

    // Last answer is stored in v2
    return v2[0];
}

// Driver Code
public static void Main(String[] args)
{
    int []a = { 1, 2, 3, 4 };
    int n = a.Length;
    int k = 3;

    Console.Write(solution(a, n, k));
}
}

// This code is contributed by Rohit_ranjan
```

## java 描述语言

```
<script>

// Function which returns the numbe of
// unique subsequences of length K
function solution(A, N, K)
{

    // Bases cases
    if (N < k || N < 1 || k < 1)
        return 0;
    if (N == k)
        return 1;

    // Prepare arrays for recursion
    let v1 = new Array(N);
    let v2 = new Array(N);
    let v3 = new Array(N);

    for(let i = 0; i < N; i++)
    {
        v1[i] = 0;
        v2[i] = 0;
        v3[i] = 0;
    }

    // Initiate separately for k = 1
    // initiate the last element
    v2[N - 1] = 1;
    v3[A[N - 1] - 1] = 1;

    // Initiate all other elements of k = 1
    for(let i = N - 2; i >= 0; i--)
    {

        // Initialize the front element
        // to vector v2
        v2[i] = v2[i + 1];

        // If element v[a[i]-1] is 0
        // then increment it in vector v2
        if (v3[A[i] - 1] == 0)
        {
            v2[i]++;
            v3[A[i] - 1] = 1;
        }
    }

    // Iterate for all possible values of K
    for(let j = 1; j < k; j++)
    {

        // Fill the vectors with 0
        for(let i = 0; i < v3.length; i++)
        {
            v3[i] = 0;
        }

        // Fill(v1.begin(), v1.end(), 0)
        // the last must be 0 as from last
        // no unique subarray can be formed
        v1[N - 1] = 0;

        // Iterate for all index from which
        // unique subsequences can be formed
        for(let i = N - 2; i >= 0; i--)
        {

            // Add the number of subsequence
            // formed from the next index
            v1[i] = v1[i + 1];

            // Start with combinations on the
            // next index
            v1[i] = v1[i] + v2[i + 1];

            // Remove the elements which have
            // already been counted
            v1[i] = v1[i] - v3[A[i] - 1];

            // Update the number used
            v3[A[i] - 1] = v2[i + 1];
        }
    }

    // Last answer is stored in v2
    return v2[0];
}

// Driver Code
let a = [ 1, 2, 3, 4 ];
let n = a.length;
let k = 3;

document.write(solution(a, n, k));

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
4
```

**时间复杂度:**O(N * K)
T3】辅助空间: O(N)