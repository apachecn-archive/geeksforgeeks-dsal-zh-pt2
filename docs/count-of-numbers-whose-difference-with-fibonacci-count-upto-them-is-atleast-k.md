# 计数与斐波那契数之差至少为 K 的数

> 原文:[https://www . geeksforgeeks . org/count-of-numbers-with-Fibonacci-count-up-them-at-k/](https://www.geeksforgeeks.org/count-of-numbers-whose-difference-with-fibonacci-count-upto-them-is-atleast-k/)

**先决条件:** [二分搜索法](https://www.geeksforgeeks.org/binary-search/)
给定两个正整数 **N** 和 **K** ，任务是统计满足以下条件的所有数字:
如果数字为 **num** ，

*   在≤ N 处。
*   **ABS(num–count)≥K**其中**计数**是到 **num** 的斐波那契数的计数。

**例:**

> **输入:** N = 10，K = 3
> **输出:** 2
> **说明:**
> 9 和 10 是满足给定条件的有效数字。
> 对于 9，9 和高达 9 (0，1，2，3，5，8)的斐波那契数之间的差值是 9–6 = 3。
> 对于 10，9 和斐波那契数到 10 (0，1，2，3，5，8)之间的差值是 10–6 = 4。
> **输入:** N = 30，K = 7
> **输出:** 11

**观察:**仔细观察，对于特定的 **K** 来说，斐波那契数与该数之差的函数是单调递增的函数。另外，如果数字 **X** 是有效数字，那么 **X + 1** 也将是有效数字。
**证明:**

> *   Let the function **c <sub>I</sub>** represent the counting of Fibonacci numbers until the number **I** .
> *   Now, for the number **x+1** , the difference is x+1–c <sub>x+1</sub> , which is greater than or equal to the difference x–c <sub>x</sub> , namely **(x+1–c <sub>x+1</sub> ).**
> *   Therefore, if **(x–c <sub>x</sub> ) ≥ s** , then **(x+1–CX+1) ≥ s** .

**方法:**因此，从上面的观察来看，想法是使用[散列](https://www.geeksforgeeks.org/hashing-data-structure/)来预计算和存储[斐波那契节点](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)直到最大值，并使用[前缀和数组概念](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)创建前缀数组，其中每个索引存储小于‘I’的斐波那契数，以使检查变得容易和高效(在 O(1)时间内)。
现在，我们可以使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)来查找最小有效数字 **X** ，因为范围[ **X** ， **N** 内的所有数字都是有效的。因此，答案是**N–X+1**。
以下是上述办法的实施:

## C++

```
// C++ program to find the count
// of numbers whose difference with
// Fibonacci count upto them is atleast K

#include <bits/stdc++.h>
using namespace std;

const int MAX = 1000005;

// fibUpto[i] denotes the count of
// fibonacci numbers upto i
int fibUpto[MAX + 1];

// Function to compute all the Fibonacci
// numbers and update fibUpto array
void compute(int sz)
{
    bool isFib[sz + 1];
    memset(isFib, false, sizeof(isFib));

    // Store the first two Fibonacci numbers
    int prev = 0, curr = 1;
    isFib[prev] = isFib[curr] = true;

    // Compute the Fibonacci numbers
    // and store them in isFib array
    while (curr <= sz) {
        int temp = curr + prev;
        isFib[temp] = true;
        prev = curr;
        curr = temp;
    }

    // Compute fibUpto array
    fibUpto[0] = 1;
    for (int i = 1; i <= sz; i++) {
        fibUpto[i] = fibUpto[i - 1];
        if (isFib[i])
            fibUpto[i]++;
    }
}

// Function to return the count
// of valid numbers
int countOfNumbers(int N, int K)
{

    // Compute fibUpto array
    compute(N);

    // Binary search to find the minimum
    // number that follows the condition
    int low = 1, high = N, ans = 0;
    while (low <= high) {
        int mid = (low + high) >> 1;

        // Check if the number is
        // valid, try to reduce it
        if (mid - fibUpto[mid] >= K) {
            ans = mid;
            high = mid - 1;
        }
        else
            low = mid + 1;
    }

    // Ans is the minimum valid number
    return (ans ? N - ans + 1 : 0);
}

// Driver Code
int main()
{
    int N = 10, K = 3;

    cout << countOfNumbers(N, K);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the count
// of numbers whose difference with
// Fibonacci count upto them is atleast K
import java.util.*;

class GFG{

static int MAX = 1000005;

// fibUpto[i] denotes the count of
// fibonacci numbers upto i
static int []fibUpto = new int[MAX + 1];

// Function to compute all the Fibonacci
// numbers and update fibUpto array
static void compute(int sz)
{
    boolean []isFib = new boolean[sz + 1];

    // Store the first two Fibonacci numbers
    int prev = 0, curr = 1;
    isFib[prev] = isFib[curr] = true;

    // Compute the Fibonacci numbers
    // and store them in isFib array
    while (curr <= sz) {
        int temp = curr + prev;
        if(temp <= sz)
            isFib[temp] = true;
        prev = curr;
        curr = temp;
    }

    // Compute fibUpto array
    fibUpto[0] = 1;
    for (int i = 1; i <= sz; i++) {
        fibUpto[i] = fibUpto[i - 1];
        if (isFib[i])
            fibUpto[i]++;
    }
}

// Function to return the count
// of valid numbers
static int countOfNumbers(int N, int K)
{

    // Compute fibUpto array
    compute(N);

    // Binary search to find the minimum
    // number that follows the condition
    int low = 1, high = N, ans = 0;
    while (low <= high) {
        int mid = (low + high) >> 1;

        // Check if the number is
        // valid, try to reduce it
        if (mid - fibUpto[mid] >= K) {
            ans = mid;
            high = mid - 1;
        }
        else
            low = mid + 1;
    }

    // Ans is the minimum valid number
    return (ans>0 ? N - ans + 1 : 0);
}

// Driver Code
public static void main(String[] args)
{
    int N = 10, K = 3;

    System.out.print(countOfNumbers(N, K));
}
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python 3 program to find the count
# of numbers whose difference with
# Fibonacci count upto them is atleast K

MAX = 1000005

# fibUpto[i] denotes the count of
# fibonacci numbers upto i
fibUpto = [0]*(MAX + 1)

# Function to compute all the Fibonacci
# numbers and update fibUpto array
def compute(sz):

    isFib = [False]*(sz + 1)
    # Store the first two Fibonacci numbers
    prev = 0
    curr = 1
    isFib[prev] = True
    isFib[curr] = True

    # Compute the Fibonacci numbers
    # and store them in isFib array
    while (curr <=sz):
        temp = curr + prev
        if(temp<=sz):
            isFib[temp] = True
        prev = curr
        curr = temp

    # Compute fibUpto array
    fibUpto[0] = 1
    for i in range( 1,sz+1):
        fibUpto[i] = fibUpto[i - 1]
        if (isFib[i]):
            fibUpto[i]+=1

# Function to return the count
# of valid numbers
def countOfNumbers(N, K):

    # Compute fibUpto array
    compute(N)

    # Binary search to find the minimum
    # number that follows the condition
    low , high, ans = 1, N, 0
    while (low <= high):
        mid = (low + high) >> 1

        # Check if the number is
        # valid, try to reduce it
        if (mid - fibUpto[mid] >= K):
            ans = mid
            high = mid - 1
        else:
            low = mid + 1

    # Ans is the minimum valid number
    if(ans):
        return (N - ans + 1)
    return 0

# Driver Code
if __name__ == "__main__":

    N = 10
    K = 3

    print(countOfNumbers(N, K))

# This code is contributed by chitranayal
```

## C#

```
// C# program to find the count
// of numbers whose difference with
// Fibonacci count upto them is atleast K
using System;

class GFG{

static int MAX = 1000005;

// fibUpto[i] denotes the count of
// fibonacci numbers upto i
static int []fibUpto = new int[MAX + 1];

// Function to compute all the Fibonacci
// numbers and update fibUpto array
static void compute(int sz)
{
    bool []isFib = new bool[sz + 1];

    // Store the first two Fibonacci numbers
    int prev = 0, curr = 1;
    isFib[prev] = isFib[curr] = true;

    // Compute the Fibonacci numbers
    // and store them in isFib array
    while (curr <= sz) {
        int temp = curr + prev;
        if(temp <= sz)
            isFib[temp] = true;
        prev = curr;
        curr = temp;
    }

    // Compute fibUpto array
    fibUpto[0] = 1;
    for (int i = 1; i <= sz; i++) {
        fibUpto[i] = fibUpto[i - 1];
        if (isFib[i])
            fibUpto[i]++;
    }
}

// Function to return the count
// of valid numbers
static int countOfNumbers(int N, int K)
{

    // Compute fibUpto array
    compute(N);

    // Binary search to find the minimum
    // number that follows the condition
    int low = 1, high = N, ans = 0;
    while (low <= high) {
        int mid = (low + high) >> 1;

        // Check if the number is
        // valid, try to reduce it
        if (mid - fibUpto[mid] >= K) {
            ans = mid;
            high = mid - 1;
        }
        else
            low = mid + 1;
    }

    // Ans is the minimum valid number
    return (ans>0 ? N - ans + 1 : 0);
}

// Driver Code
public static void Main()
{
    int N = 10, K = 3;

    Console.WriteLine(countOfNumbers(N, K));
}
}

// This code is contributed by Mohitkumar29
```

## java 描述语言

```
<script>
// Javascript program to find the count
// of numbers whose difference with
// Fibonacci count upto them is atleast K
let MAX = 1000005;

// fibUpto[i] denotes the count of
// fibonacci numbers upto i
let fibUpto = new Array(MAX+1);

// Function to compute all the Fibonacci
// numbers and update fibUpto array
function compute(sz)
{
    let isFib = new Array(sz + 1);

    // Store the first two Fibonacci numbers
    let prev = 0, curr = 1;
    isFib[prev] = isFib[curr] = true;

    // Compute the Fibonacci numbers
    // and store them in isFib array
    while (curr <= sz) {
        let temp = curr + prev;
        if(temp <= sz)
            isFib[temp] = true;
        prev = curr;
        curr = temp;
    }

    // Compute fibUpto array
    fibUpto[0] = 1;
    for (let i = 1; i <= sz; i++) {
        fibUpto[i] = fibUpto[i - 1];
        if (isFib[i])
            fibUpto[i]++;
    }
}

// Function to return the count
// of valid numbers
function countOfNumbers(N,K)
{
    // Compute fibUpto array
    compute(N);

    // Binary search to find the minimum
    // number that follows the condition
    let low = 1, high = N, ans = 0;
    while (low <= high) {
        let mid = (low + high) >> 1;

        // Check if the number is
        // valid, try to reduce it
        if (mid - fibUpto[mid] >= K) {
            ans = mid;
            high = mid - 1;
        }
        else
            low = mid + 1;
    }

    // Ans is the minimum valid number
    return (ans>0 ? N - ans + 1 : 0);
}

// Driver Code
let N = 10, K = 3;
document.write(countOfNumbers(N, K));

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
2
```