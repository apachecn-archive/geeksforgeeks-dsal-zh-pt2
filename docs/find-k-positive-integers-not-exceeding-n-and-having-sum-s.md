# 求不超过 N 且和为 S 的 K 个正整数

> 原文:[https://www . geesforgeks . org/find-k-正整数-不超过-n-和-having-sum-s/](https://www.geeksforgeeks.org/find-k-positive-integers-not-exceeding-n-and-having-sum-s/)

给定三个正整数 **S，K，**和 **N** ，任务是找到 **K** 个不同的正整数，不超过 **N** 且和等于**S。**如果找不到 **K** 个这样的正整数，打印 **-1** 。

**示例:**

> **输入:** S = 15，K = 4，N = 8
> **输出:** 1 2 4 8
> **解释:**
> 一组可能的 K 这样的数字是{1，2，3，4}(自，1 + 2 + 4 + 8 =15)。
> 其他可能的 K 数集合有{2，3，4，6}、{1，3，4，7}等。
> 
> **输入:** S = 14，K = 5，N = 6
> T3】输出: -1

**方法:**按照以下步骤解决问题:

*   如果 **N** 小于 **K** ，则打印 **-1** 。
*   如果 **S** 小于第一个 **K** 自然数的[和，即(1 + 2 + … + K)或者如果 **S** 大于最后一个**K**T10】自然数](https://www.geeksforgeeks.org/program-find-sum-first-n-natural-numbers/)的和，即从 **N** 到**N–K+1**，则打印 **-1** 。
*   从 **1** 开始迭代，不断将变量中遇到的每个自然数相加，比如说 **s1** ，而 **s1 ≤ S.** 将遇到的所有元素插入一个数组中，比如说 **nums[]** 。
*   从**nums【】**中提取**K–1**元素并存储在另一个数组中，说**回答**。
*   阵列**答案【】**中的第 **K <sup>个</sup>元素将为**(S1–S2)**，其中 **s2** 是阵列**答案【】**中存在的**K–1**个元素之和。**
*   [反向遍历阵](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **回答【】**，将所有阵元减少到小于等于 **N** 。

下面是上述方法的实现:

## C++

```
// C++ implementation
// for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to represent S as
// the sum of K positive integers
// less than or equal to N
void solve(int S, int K, int N)
{
    if (K > N) {
        cout << "-1" << endl;
        return;
    }

    int max_sum = 0, min_sum = 0;

    for (int i = 1; i <= K; i++) {
        min_sum += i;
        max_sum += N - i + 1;
    }

    // If S can cannot be represented
    // as sum of K integers
    if (S < min_sum || S > max_sum) {
        cout << "-1" << endl;
        return;
    }

    int s1 = 0;

    vector<int> nums;

    for (int i = 1; i <= N; i++) {

        // If sum of first i natural
        // numbers exceeds S
        if (s1 > S)
            break;

        s1 += i;

        // Insert i into nums[]
        nums.push_back(i);
    }

    vector<int> answer;
    int s2 = 0;

    // Insert first K - 1 positive
    // numbers into answer[]
    for (int i = 0; i < K - 1; i++) {
        answer.push_back(nums[i]);
        s2 += nums[i];
    }

    // Insert the K-th number
    answer.push_back(S - s2);

    int Max = N;

    // Traverse the array answer[]
    for (int i = answer.size() - 1; i >= 0; i--) {

        // If current element exceeds N
        if (answer[i] > Max) {

            int extra = answer[i] - Max;

            // Add the extra value to
            // the previous element
            if (i - 1 >= 0)
                answer[i - 1] += extra;

            // Reduce current element to N
            answer[i] = Max;

            Max--;
        }

        else
            break;
    }

    // Printing the K numbers
    for (auto x : answer)
        cout << x << " ";

    cout << endl;
}

// Driver Code
int main()
{
    int S = 15, K = 4, N = 8;
    solve(S, K, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation
// for the above approach
import java.util.Vector;

class GFG{

// Function to represent S as
// the sum of K positive integers
// less than or equal to N
static void solve(int S, int K, int N)
{
    if (K > N)
    {
        System.out.println("-1");
        return;
    }

    int max_sum = 0, min_sum = 0;

    for(int i = 1; i <= K; i++)
    {
        min_sum += i;
        max_sum += N - i + 1;
    }

    // If S can cannot be represented
    // as sum of K integers
    if (S < min_sum || S > max_sum)
    {
        System.out.println("-1");
        return;
    }

    int s1 = 0;

    Vector<Integer> nums = new Vector<>();

    for(int i = 1; i <= N; i++)
    {

        // If sum of first i natural
        // numbers exceeds S
        if (s1 > S)
            break;

        s1 += i;

        // Insert i into nums[]
        nums.add(i);
    }
    Vector<Integer> answer = new Vector<>();
    int s2 = 0;

    // Insert first K - 1 positive
    // numbers into answer[]
    for(int i = 0; i < K - 1; i++)
    {
        answer.add(nums.get(i));
        s2 += nums.get(i);
    }

    // Insert the K-th number
    answer.add(S - s2);

    int Max = N;

    // Traverse the array answer[]
    for(int i = answer.size() - 1;
            i >= 0; i--)
    {

        // If current element exceeds N
        if (answer.get(i) > Max)
        {
            int extra = answer.get(i) - Max;

            // Add the extra value to
            // the previous element
            if (i - 1 >= 0)
                answer.set(i - 1,
                answer.get(i - 1) + extra);

            // Reduce current element to N
            answer.set(i, Max);

            Max--;
        }
        else
            break;
    }

    // Printing the K numbers
    for(int x : answer)
        System.out.print(x + " ");

    System.out.println();
}

// Driver code
public static void main(String[] args)
{
    int S = 15, K = 4, N = 8;

    solve(S, K, N);
}
}

// This code is contributed by abhinavjain194
```

## 蟒蛇 3

```
# Python3 implementation
# for the above approach

# Function to represent S as
# the sum of K positive integers
# less than or equal to N
def solve(S, K, N):
    if (K > N):
        print("-1")
        return

    max_sum, min_sum = 0, 0

    for i in range(K + 1):
        min_sum += i
        max_sum += N - i + 1

    # If S can cannot be represented
    # as sum of K integers
    if (S < min_sum or S > max_sum):
        print("-1")
        return

    s1 = 0

    nums = []

    for i in range(1, N + 1):

        # If sum of first i natural
        # numbers exceeds S
        if (s1 > S):
            break

        s1 += i

        # Insert i into nums[]
        nums.append(i)

    answer = []
    s2 = 0

    # Insert first K - 1 positive
    # numbers into answer[]
    for i in range(K - 1):
        answer.append(nums[i])
        s2 += nums[i]

    # Insert the K-th number
    answer.append(S - s2)

    Max = N

    # Traverse the array answer[]
    for i in range(len(answer)-1,-1,-1):

        # If current element exceeds N
        if (answer[i] > Max):

            extra = answer[i] - Max

            # Add the extra value to
            # the previous element
            if (i - 1 >= 0):
                answer[i - 1] += extra

            # Reduce current element to N
            answer[i] = Max

            Max -= 1
        else:
            break

    # Printing the K numbers
    for x in answer:
        print(x, end = " ")

# Driver Code
if __name__ == '__main__':
    S,K,N = 15, 4, 8
    solve(S, K, N)

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# implementation
// for the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to represent S as
// the sum of K positive integers
// less than or equal to N
static void solve(int S, int K, int N)
{
    if (K > N)
    {
        Console.WriteLine("-1");
        return;
    }

    int max_sum = 0, min_sum = 0;

    for(int i = 1; i <= K; i++)
    {
        min_sum += i;
        max_sum += N - i + 1;
    }

    // If S can cannot be represented
    // as sum of K integers
    if (S < min_sum || S > max_sum)
    {
        Console.WriteLine("-1");
        return;
    }

    int s1 = 0;
    List<int> nums = new List<int>();

    for(int i = 1; i <= N; i++)
    {

        // If sum of first i natural
        // numbers exceeds S
        if (s1 > S)
            break;

        s1 += i;

        // Insert i into nums[]
        nums.Add(i);
    }

    List<int> answer = new List<int>();
    int s2 = 0;

    // Insert first K - 1 positive
    // numbers into answer[]
    for(int i = 0; i < K - 1; i++)
    {
        answer.Add(nums[i]);
        s2 += nums[i];
    }

    // Insert the K-th number
    answer.Add(S - s2);

    int Max = N;

    // Traverse the array answer[]
    for(int i = answer.Count - 1; i >= 0; i--)
    {

        // If current element exceeds N
        if (answer[i] > Max)
        {
            int extra = answer[i] - Max;

            // Add the extra value to
            // the previous element
            if (i - 1 >= 0)
                answer[i - 1] += extra;

            // Reduce current element to N
            answer[i] = Max;

            Max--;
        }
        else
            break;
    }

    // Printing the K numbers
    foreach(int x in answer)
        Console.Write(x + " ");

    Console.WriteLine();
}

// Driver Code
public static void Main()
{
    int S = 15, K = 4, N = 8;
    solve(S, K, N);
}
}

// This code is contributed by ukasp
```

## java 描述语言

```
<script>

// Javascript implementation
// for the above approach

// Function to represent S as
// the sum of K positive integers
// less than or equal to N
function solve(S, K, N)
{
    if (K > N)
    {
        document.write("-1");
        return;
    }

    let max_sum = 0, min_sum = 0;

    for(let i = 1; i <= K; i++)
    {
        min_sum += i;
        max_sum += N - i + 1;
    }

    // If S can cannot be represented
    // as sum of K integers
    if (S < min_sum || S > max_sum)
    {
        document.write("-1");
        return;
    }

    let s1 = 0;
    let nums = [];

    for(let i = 1; i <= N; i++)
    {

        // If sum of first i natural
        // numbers exceeds S
        if (s1 > S)
            break;

        s1 += i;

        // Insert i into nums[]
        nums.push(i);
    }

    let answer = [];
    let s2 = 0;

    // Insert first K - 1 positive
    // numbers into answer[]
    for(let i = 0; i < K - 1; i++)
    {
        answer.push(nums[i]);
        s2 += nums[i];
    }

    // Insert the K-th number
    answer.push(S - s2);

    let Max = N;

    // Traverse the array answer[]
    for(let i = answer.length - 1; i >= 0; i--)
    {

        // If current element exceeds N
        if (answer[i] > Max)
        {
            let extra = answer[i] - Max;

            // Add the extra value to
            // the previous element
            if (i - 1 >= 0)
                answer[i - 1] += extra;

            // Reduce current element to N
            answer[i] = Max;

            Max--;
        }
        else
            break;
    }

    // Printing the K numbers
    for(let x in answer)
        document.write(answer[x] + " ");

    document.write("<br/>");
}

// Driver Code

    let S = 15, K = 4, N = 8;
    solve(S, K, N);

 // This code is contributed by susmitakundugoaldanga.
</script>
```

**Output:** 

```
1 2 4 8
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)