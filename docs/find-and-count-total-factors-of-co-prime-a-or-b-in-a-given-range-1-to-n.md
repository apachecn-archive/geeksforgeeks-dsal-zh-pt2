# 找出并计算给定范围 1 到 N 内共质数 A 或 B 的总因子

> 原文:[https://www . geesforgeks . org/find-and-count-total-of-factors-co-prime-a-或-b-in-给定范围-1-n/](https://www.geeksforgeeks.org/find-and-count-total-factors-of-co-prime-a-or-b-in-a-given-range-1-to-n/)

给定三个整数 N，A，B，当[1，N]范围内可被 A 或 B 整除的整数之和除以该范围内的整数数时，任务就是求余数。
**注:**数字 A 和 B 是同素的。
**示例:**

> **输入:** N = 88，A = 11，B = 8
> **输出:** 8
> **说明:**
> 在[1，88]范围内总共有 18 个数字可以被 8 或 11 整除。它们是:
> { 8、11、16、22、24、32、33、40、44、48、55、56、64、66、72、77、80、88 }。因此，这些数字的总和是 836。因此，836 % 18 = 8。
> **输入:** N = 100，A = 7，B = 19
> **输出:** 13
> **说明:**
> 在[1，100]范围内共有 19 个数字可以被 7 或 19 整除。它们是:
> { 7，14，19，21，28，35，38，42，49，56，57，63，70，76，77，84，91，95，98 }。因此，这些数字的总和是 1020。因此，1020 % 19 = 13。

**天真方法:**天真方法是运行一个从 1 到 N 的循环，计算所有可被 A 或 B 整除的数字，同时将变量中的这些数字相加，以找到其和。
**时间复杂度:** O(N)
**高效进场:**高效进场就是用除法的方法。

*   利用除法，可以在常数时间内找到被 **A** 或 **B** 整除的**数**的**计数。这个想法是:**
    1.  **将 N 除以 A** 得到【1，N】范围内可被 **A** 整除的数字个数。
    2.  **将 N 除以 B** 得到【1，N】范围内可被 **B** 整除的数字个数。
    3.  **将 N 除以 A * B** 得到可被**A 和 B** 整除的数字个数。
    4.  **将**第一步和第二步**得到的值相加**，将**第三步**得到的值减去，去掉已经计算了两次的数字。
*   因为我们甚至有兴趣在这个范围内找到可被整除的**数，所以我们的想法是通过以下方式减少条件检查的次数:**
    *   不完全依赖一个循环，我们可以用**两个循环**。
    *   一个循环是找到能被 **A** 整除的数。我们不是将值增加 1，而是从 A 开始循环，并将其增加 1。这大大减少了比较的次数。
    *   同样，另一个循环用于寻找可被 **B** 整除的数字。
    *   同样，由于数字中可能有重复，因此数字存储在[设置](https://www.geeksforgeeks.org/set-in-cpp-stl/)中，因此没有重复。
*   一旦找到了数字的计数和总和，就可以直接进行模运算来计算最终答案。

以下是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ implementation of the above approach
#include <algorithm>
#include <iostream>
#include <set>
#define ll long long
using namespace std;

// Function to return the count of numbers
// which are divisible by both A and B in
// the range [1, N] in constant time
ll int countOfNum(ll int n, ll int a, ll int b)
{
    ll int cnt_of_a, cnt_of_b, cnt_of_ab, sum;

    // Compute the count of numbers divisible by
    // A in the range [1, N]
    cnt_of_a = n / a;

    // Compute the count of numbers divisible by
    // B in the range [1, N]
    cnt_of_b = n / b;

    // Adding the counts which are
    // divisible by A and B
    sum = cnt_of_b + cnt_of_a;

    // The above value might contain repeated
    // values which are divisible by both
    // A and B. Therefore, the count of numbers
    // which are divisible by both A and B are found
    cnt_of_ab = n / (a * b);

    // The count computed above is subtracted to
    // compute the final count
    sum = sum - cnt_of_ab;

    return sum;
}

// Function to return the sum of numbers
// which are divisible by both A and B
// in the range [1, N]
ll int sumOfNum(ll int n, ll int a, ll int b)
{
    ll int i;
    ll int sum = 0;

    // Set to store the numbers so that the
    // numbers are not repeated
    set<ll int> ans;

    // For loop to find the numbers
    // which are divisible by A and insert
    // them into the set
    for (i = a; i <= n; i = i + a) {
        ans.insert(i);
    }

    // For loop to find the numbers
    // which are divisible by A and insert
    // them into the set
    for (i = b; i <= n; i = i + b) {
        ans.insert(i);
    }

    // For loop to iterate through the set
    // and find the sum
    for (auto it = ans.begin();
         it != ans.end(); it++) {
        sum = sum + *it;
    }

    return sum;
}

// Driver code
int main()
{
    ll int N = 88;
    ll int A = 11;
    ll int B = 8;

    ll int count = countOfNum(N, A, B);
    ll int sumofnum = sumOfNum(N, A, B);

    cout << sumofnum % count << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach

import java.util.*;
// Function to return the count of numbers
// which are divisible by both A and B in
// the range [1, N] in constant time

class GFG
{

    static int countOfNum( int n,  int a, int b)
    {
        int cnt_of_a, cnt_of_b, cnt_of_ab, sum;

        // Compute the count of numbers divisible by
        // A in the range [1, N]
        cnt_of_a = n / a;

        // Compute the count of numbers divisible by
        // B in the range [1, N]
        cnt_of_b = n / b;

        // Adding the counts which are
        // divisible by A and B
        sum = cnt_of_b + cnt_of_a;

        // The above value might contain repeated
        // values which are divisible by both
        // A and B. Therefore, the count of numbers
        // which are divisible by both A and B are found
        cnt_of_ab = n / (a * b);

        // The count computed above is subtracted to
        // compute the final count
        sum = sum - cnt_of_ab;

        return sum;
    }

    // Function to return the sum of numbers
    // which are divisible by both A and B
    // in the range [1, N]
    static int sumOfNum( int n,  int a, int b)
    {
        int i;
        int sum = 0;

        // Set to store the numbers so that the
        // numbers are not repeated
        Set< Integer> ans =  new HashSet<Integer>();

        // For loop to find the numbers
        // which are divisible by A and insert
        // them into the set
        for (i = a; i <= n; i = i + a) {
            ans.add(i);
        }

        // For loop to find the numbers
        // which are divisible by A and insert
        // them into the set
        for (i = b; i <= n; i = i + b) {
            ans.add(i);
        }

        // For loop to iterate through the set
        // and find the sum
        for (Integer it : ans) {
            sum = sum + it;
        }

        return sum;
    }

    // Driver code
    public static void main (String []args)
    {
        int N = 88;
        int A = 11;
        int B = 8;

        int count = countOfNum(N, A, B);
        int sumofnum = sumOfNum(N, A, B);

        System.out.print(sumofnum % count);
    }
}

// This code is contributed by chitranayal 
```

## 蟒蛇 3

```
# Python3 implementation of the above approach

# Function to return the count of numbers
# which are divisible by both A and B in
# the range [1, N] in constant time
def countOfNum(n, a, b):
    cnt_of_a, cnt_of_b, cnt_of_ab, sum = 0, 0, 0, 0

    # Compute the count of numbers divisible by
    # A in the range [1, N]
    cnt_of_a = n // a

    # Compute the count of numbers divisible by
    # B in the range [1, N]
    cnt_of_b = n // b

    # Adding the counts which are
    # divisible by A and B
    sum = cnt_of_b + cnt_of_a

    # The above value might contain repeated
    # values which are divisible by both
    # A and B. Therefore, the count of numbers
    # which are divisible by both A and B are found
    cnt_of_ab = n // (a * b)

    # The count computed above is subtracted to
    # compute the final count
    sum = sum - cnt_of_ab

    return sum

# Function to return the sum of numbers
# which are divisible by both A and B
# in the range [1, N]
def sumOfNum(n, a, b):

    i = 0
    sum = 0

    # Set to store the numbers so that the
    # numbers are not repeated
    ans = dict()

    # For loop to find the numbers
    # which are divisible by A and insert
    # them into the set
    for i in range(a, n + 1, a):
        ans[i] = 1

    # For loop to find the numbers
    # which are divisible by A and insert
    # them into the set
    for i in range(b, n + 1, b):
        ans[i] = 1

    # For loop to iterate through the set
    # and find the sum
    for it in ans:
        sum = sum + it
    return sum

# Driver code
if __name__ == '__main__':
    N = 88
    A = 11
    B = 8

    count = countOfNum(N, A, B)
    sumofnum = sumOfNum(N, A, B)

    print(sumofnum % count)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the above approach
using System;
using System.Collections.Generic;

class GFG
{
    // Function to return the count of numbers
    // which are divisible by both A and B in
    // the range [1, N] in constant time

    static int countOfNum( int n,  int a, int b)
    {
        int cnt_of_a, cnt_of_b, cnt_of_ab, sum;

        // Compute the count of numbers divisible by
        // A in the range [1, N]
        cnt_of_a = n / a;

        // Compute the count of numbers divisible by
        // B in the range [1, N]
        cnt_of_b = n / b;

        // Adding the counts which are
        // divisible by A and B
        sum = cnt_of_b + cnt_of_a;

        // The above value might contain repeated
        // values which are divisible by both
        // A and B. Therefore, the count of numbers
        // which are divisible by both A and B are found
        cnt_of_ab = n / (a * b);

        // The count computed above is subtracted to
        // compute the readonly count
        sum = sum - cnt_of_ab;

        return sum;
    }

    // Function to return the sum of numbers
    // which are divisible by both A and B
    // in the range [1, N]
    static int sumOfNum( int n,  int a, int b)
    {
        int i;
        int sum = 0;

        // Set to store the numbers so that the
        // numbers are not repeated
        HashSet< int> ans =  new HashSet<int>();

        // For loop to find the numbers
        // which are divisible by A and insert
        // them into the set
        for (i = a; i <= n; i = i + a) {
            ans.Add(i);
        }

        // For loop to find the numbers
        // which are divisible by A and insert
        // them into the set
        for (i = b; i <= n; i = i + b) {
            ans.Add(i);
        }

        // For loop to iterate through the set
        // and find the sum
        foreach (int it in ans) {
            sum = sum + it;
        }

        return sum;
    }

    // Driver code
    public static void Main(String []args)
    {
        int N = 88;
        int A = 11;
        int B = 8;

        int count = countOfNum(N, A, B);
        int sumofnum = sumOfNum(N, A, B);

        Console.Write(sumofnum % count);
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript implementation of the above approach

    // Function to return the count of numbers
    // which are divisible by both A and B in
    // the range [1, N] in constant time
    function countOfNum(n,a,b)
    {
        let cnt_of_a, cnt_of_b, cnt_of_ab, sum;

        // Compute the count of numbers divisible by
        // A in the range [1, N]
        cnt_of_a = Math.floor(n / a);

        // Compute the count of numbers divisible by
        // B in the range [1, N]
        cnt_of_b = Math.floor(n / b);

        // Adding the counts which are
        // divisible by A and B
        sum = cnt_of_b + cnt_of_a;

        // The above value might contain repeated
        // values which are divisible by both
        // A and B. Therefore, the count of numbers
        // which are divisible by both A and B are found
        cnt_of_ab = Math.floor(n / (a * b));

        // The count computed above is subtracted to
        // compute the final count
        sum = sum - cnt_of_ab;

        return sum;
    }

    // Function to return the sum of numbers
    // which are divisible by both A and B
    // in the range [1, N]
    function sumOfNum(n,a,b)
    {
        let i;
        let sum = 0;

        // Set to store the numbers so that the
        // numbers are not repeated
        let ans =  new Set();

        // For loop to find the numbers
        // which are divisible by A and insert
        // them into the set
        for (i = a; i <= n; i = i + a) {
            ans.add(i);
        }

        // For loop to find the numbers
        // which are divisible by A and insert
        // them into the set
        for (i = b; i <= n; i = i + b) {
            ans.add(i);
        }

        // For loop to iterate through the set
        // and find the sum
        for (let it of ans.values()) {
            sum = sum + it;
        }

        return sum;
    }

    // Driver code
    let N = 88;
    let A = 11;
    let B = 8;

   let count = countOfNum(N, A, B);
    let sumofnum = sumOfNum(N, A, B);

    document.write(sumofnum % count);

    // This code is contributed by rag2127
</script>
```

**Output:** 

```
8
```

**时间复杂度分析:**

*   运行 for 循环寻找可被 A 整除的数字所花费的时间为 **O(N / A)** 。
*   运行 for 循环以找到可被 B 整除的数字所花费的时间是 **O(N / B)** 。
*   因此，整体时间复杂度为 **O(N / A) + O(N / B)** 。

**辅助空间:** O(N/A + N/B)