# 和等于 N 的阶乘的最小个数

> 原文:[https://www . geesforgeks . org/最小阶乘数-其和等于-n/](https://www.geeksforgeeks.org/minimum-number-of-factorials-whose-sum-is-equal-to-n/)

给定一个数 **N** ( < 10 <sup>10</sup> ，任务是找到表示 N 所需的最小阶乘数，作为它们的和。另外，打印那些阶乘。
**例:**

```
Input: N = 30
Output: 2
24, 6
Explanation:
Factorials needed to represent 30: 24, 6

Input: N = 150
Output: 3
120, 24, 6
Explanation:
Factorials needed to represent 150: 120 24 6
```

**接近** :

1.  为了高效地[找到将 N 表示为其和所需的阶乘](https://www.geeksforgeeks.org/find-factorial-numbers-less-equal-n/)，我们可以预先计算阶乘直到 N (N < 10 <sup>10</sup> )并将它们存储在数组中，以便更快地计算。

2.  然后使用[贪婪算法](https://www.geeksforgeeks.org/greedy-algorithms/)，我们可以从这个数组中取最大的阶乘，可以加起来表示 N.

3.  从最大可能的阶乘开始，当剩余值大于 0 时，继续添加阶乘。

4.  下面是完整的算法。
    *   将结果初始化为空
    *   找出小于 N 的最大阶乘
    *   将找到的阶乘添加到结果中。从 N 中减去找到的阶乘的值
    *   如果 N 变为 0，则打印结果。否则，对新的 N 值重复步骤 2 和 3

以下是上述方法的实现:

## C++

```
// C++ program to find minimum number of factorials

#include <bits/stdc++.h>
#define ll long long int
using namespace std;

// Array to calculate all factorials
// less than or equal to N
// Since there can be only 14 factorials
// till 10^10
// Hence the maximum size of fact[] is 14
ll fact[14];

// Store the actual size of fact[]
int size = 1;

// Function to precompute factorials till N
void preCompute(int N)
{
    // Precomputing factorials
    fact[0] = 1;

    for (int i = 1; fact[i - 1] <= N; i++) {
        fact[i] = (fact[i - 1] * i);
        size++;
    }
}

// Function to find the minimum number
// of factorials whose sum represents N
void findMin(int N)
{

    // Precompute factorials
    preCompute(N);

    int originalN = N;

    // Initialize result
    vector<int> ans;

    // Traverse through all factorials
    for (int i = size - 1; i >= 0; i--) {

        // Find factorials
        while (N >= fact[i]) {
            N -= fact[i];
            ans.push_back(fact[i]);
        }
    }

    // Print min count
    cout << ans.size() << "\n";

    // Print result
    for (int i = 0; i < ans.size(); i++)
        cout << ans[i] << " ";
}

// Driver program
int main()
{
    int n = 27;
    findMin(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum number of factorials
import java.util.*;

class GFG{

// Array to calculate all factorials
// less than or equal to N
// Since there can be only 14 factorials
// till 10^10
// Hence the maximum size of fact[] is 14
static int []fact = new int[14];

// Store the actual size of fact[]
static int size = 1;

// Function to precompute factorials till N
static void preCompute(int N)
{
    // Precomputing factorials
    fact[0] = 1;

    for (int i = 1; fact[i - 1] <= N; i++) {
        fact[i] = (fact[i - 1] * i);
        size++;
    }
}

// Function to find the minimum number
// of factorials whose sum represents N
static void findMin(int N)
{

    // Precompute factorials
    preCompute(N);

    int originalN = N;

    // Initialize result
    Vector<Integer> ans = new Vector<Integer>();

    // Traverse through all factorials
    for (int i = size - 1; i >= 0; i--) {

        // Find factorials
        while (N >= fact[i]) {
            N -= fact[i];
            ans.add(fact[i]);
        }
    }

    // Print min count
    System.out.print(ans.size()+ "\n");

    // Print result
    for (int i = 0; i < ans.size(); i++)
        System.out.print(ans.get(i)+ " ");
}

// Driver program
public static void main(String[] args)
{
    int n = 27;
    findMin(n);
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program to find minimum number of factorials

# Array to calculate all factorials
# less than or equal to N
# Since there can be only 14 factorials
# till 10^10
# Hence the maximum size of fact[] is 14
fact = [0]*14

# Store the actual size of fact[]
size = 1

# Function to precompute factorials till N
def preCompute(N):
    global size

    # Precomputing factorials
    fact[0] = 1

    i = 1

    while fact[i - 1] <= N:
        fact[i] = fact[i - 1] * i
        size += 1
        i += 1

# Function to find the minimum number
# of factorials whose sum represents N
def findMin(N):

    # Precompute factorials

    preCompute(N)

    originalN = N

    # Initialize result
    ans = []

    # Traverse through all factorials
    for i in range(size-1, -1, -1):

        # Find factorials
        while (N >= fact[i]):
            N -= fact[i]
            ans.append(fact[i])

    # Prmin count
    print(len(ans))

    # Prresult
    for i in ans:
        print(i, end=" ")

# Driver program

n = 27
findMin(n)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to find minimum number of factorials
using System;
using System.Collections.Generic;

class GFG{

// Array to calculate all factorials
// less than or equal to N
// Since there can be only 14 factorials
// till 10^10
// Hence the maximum size of fact[] is 14
static int []fact = new int[14];

// Store the actual size of fact[]
static int size = 1;

// Function to precompute factorials till N
static void preCompute(int N)
{
    // Precomputing factorials
    fact[0] = 1;

    for (int i = 1; fact[i - 1] <= N; i++) {
        fact[i] = (fact[i - 1] * i);
        size++;
    }
}

// Function to find the minimum number
// of factorials whose sum represents N
static void findMin(int N)
{

    // Precompute factorials
    preCompute(N);

    int originalN = N;

    // Initialize result
    List<int> ans = new List<int>();

    // Traverse through all factorials
    for (int i = size - 1; i >= 0; i--) {

        // Find factorials
        while (N >= fact[i]) {
            N -= fact[i];
            ans.Add(fact[i]);
        }
    }

    // Print min count
    Console.Write(ans.Count+ "\n");

    // Print result
    for (int i = 0; i < ans.Count; i++)
        Console.Write(ans[i]+ " ");
}

// Driver program
public static void Main(String[] args)
{
    int n = 27;
    findMin(n);
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript program to find minimum number of factorials

// Array to calculate all factorials
// less than or equal to N
// Since there can be only 14 factorials
// till 10^10
// Hence the maximum size of fact[] is 14
var fact = Array(14).fill(0);

// Store the actual size of fact[]
var size = 1;

// Function to precompute factorials till N
function preCompute(N)
{
    // Precomputing factorials
    fact[0] = 1;

    for (var i = 1; fact[i - 1] <= N; i++) {
        fact[i] = (fact[i - 1] * i);
        size++;
    }
}

// Function to find the minimum number
// of factorials whose sum represents N
function findMin(N)
{

    // Precompute factorials
    preCompute(N);

    var originalN = N;

    // Initialize result
    ans = [];

    // Traverse through all factorials
    for (var i = size - 1; i >= 0; i--) {

        // Find factorials
        while (N >= fact[i]) {
            N -= fact[i];
            ans.push(fact[i]);
        }
    }

    // Print min count
    document.write(ans.length + "<br>");

    // Print result
    for (var i = 0; i < ans.length; i++)
        document.write(ans[i] + " ");
}

// Driver program
var n = 27;
findMin(n);

// This code is contributed by rutvik_56.
</script>
```

**Output:** 

```
3
24 2 1
```

时间复杂度:0(N *大小)

辅助空间:0(N *大小)