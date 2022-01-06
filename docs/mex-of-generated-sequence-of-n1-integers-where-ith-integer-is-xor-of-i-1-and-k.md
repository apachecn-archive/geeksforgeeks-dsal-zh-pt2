# 生成的 N+1 整数序列的 MEX，其中 I 是(i-1)和 K 的异或

> 原文:[https://www . geesforgeks . org/MEX-of-generated-sequence-of-n1-integers-其中-ith-integer-is-xor-of-I-1-and-k/](https://www.geeksforgeeks.org/mex-of-generated-sequence-of-n1-integers-where-ith-integer-is-xor-of-i-1-and-k/)

给定两个整数 **N** 和 **K** ，生成一个大小为 **N+1** 的序列，其中**I<sup>th</sup>T9】元素为 **(i-1)⊕K** ，任务是找到该序列的 **MEX** 。这里，序列的 **MEX** 是序列中不出现的最小非负整数。**

**示例:**

> **输入** : N = 7，K=3
> **输出** : 8
> **说明:**给定 n 和 k 组成的序列是{0⊕3、1⊕3、2⊕3、3⊕3、4⊕3、5⊕3、6⊕3、7⊕3}即{3、2、1、0、7、6、5、4}
> 给定序列中不存在的最小非负数是 8
> 
> **输入:** N = 6，K = 4
> T3】输出: 3

**天真法:**解决这个问题最简单的方法就是简单的制作给定的数组并计算其 **MEX** 。以下是解决此问题的步骤:

1.  生成序列并排序。
2.  将 **MEX** 初始化为 0，并迭代排序后的数组，如果当前元素等于 **MEX** 则将 **MEX** 增加 1，否则中断循环。
3.  打印 **MEX** 作为这个问题的答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the MEX of sequence
int findMex(int N, int K)
{

    // Generating the sequence
    int A[N + 1];
    for (int i = 0; i <= N; i++) {
        A[i] = i ^ K;
    }

    // Sorting the array
    sort(A, A + N + 1);

    // Calculating the MEX
    // Initialising the MEX variable
    int MEX = 0;
    for (int x : A) {
        if (x == MEX) {

            // If current MEX is equal
            // to the element
            // increase MEX by one
            MEX++;
        }
        else {
            // If current MEX is not equal
            // to the element then
            // the current MEX is the answer
            break;
        }
    }
    return MEX;
}

// Driver code
int main()
{
    // Given Input
    int N = 7, K = 3;
    cout << findMex(N, K);
    return 0;
}
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find the MEX of sequence
static int findMex(int N, int K)
{

    // Generating the sequence
    int[] A = new int[N + 1];
    for(int i = 0; i <= N; i++)
    {
        A[i] = i ^ K;
    }

    // Sorting the array
    Array.Sort(A);

    // Calculating the MEX
    // Initialising the MEX variable
    int MEX = 0;
    foreach(int x in A)
    {
        if (x == MEX)
        {

            // If current MEX is equal
            // to the element
            // increase MEX by one
            MEX++;
        }
        else
        {

            // If current MEX is not equal
            // to the element then
            // the current MEX is the answer
            break;
        }
    }
    return MEX;
}

// Driver code
public static void Main()
{

    // Given Input
    int N = 7, K = 3;

    Console.WriteLine(findMex(N, K));
}
}

// This code is contributed by ukasp
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find the MEX of sequence
function findMex(N, K) {

    // Generating the sequence
    let A = new Array(N + 1);
    for (let i = 0; i <= N; i++) {
        A[i] = i ^ K;
    }

    // Sorting the array
    A.sort();

    // Calculating the MEX
    // Initialising the MEX variable
    let MEX = 0;
    for (x of A) {
        if (x == MEX) {

            // If current MEX is equal
            // to the element
            // increase MEX by one
            MEX++;
        }
        else {
            // If current MEX is not equal
            // to the element then
            // the current MEX is the answer
            break;
        }
    }
    return MEX;
}

// Driver code

// Given Input
let N = 7
let K = 3;
document.write(findMex(N, K))

// This code is contributed by gfgking.
</script>
```

**Output**

```
8
```

***时间复杂度:*****O(N * log(N))
***辅助空间:*** O(N)**

****有效方法:**如果一个数 **M** 以此顺序出现，那么对于某些**I<sup>th</sup>T7】项 **(i-1)⊕K = M** ，这也意味着 **M⊕K = (i-1)** ，其中( **i-1)** 的最大值为 **N** 。现在，假设 **X** 是给定序列的 MEX，那么 **X⊕K** 必须大于 **N** ，即 **X⊕K > N.** 所以， **X** 的最小值是序列的 MEX。按照以下步骤，解决这个问题:****

1.  **从后开始遍历 **N+1** 和 **K** 的位。**
2.  **如果 **K** 的 **i <sup>第</sup>T3】位等于 **N+1 的 **i <sup>第</sup>T9】位，**将 **X** 的 **i <sup>第</sup>T15】位设置为 0。********
3.  如果 **K** 的 **i <sup>第</sup>T3】位等于 **0** 且 **N+1** 的 **i <sup>第</sup>T11】位等于 1，则将 **X** 的 **i <sup>第</sup>T17】位设置为 1。******
4.  如果 **K** 的 **i <sup>第</sup>T3】位等于 **1** 并且 **N+1** 的 **i <sup>第</sup>位等于 **0** ，则将 **X** 的所有剩余低位设置为 0，因为这意味着在该位置包含设置位的数字丢失，并且它是序列的 MEX。****
5.  根据以上观察打印答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the MEX of the sequence
int findMEX(int N, int K)
{

    // Calculating the last possible bit
    int lastBit = max(round(log2(N + 1)),
                      round(log2(K)));

    // Initialising X
    int X = 0;

    for (int i = lastBit; i >= 0; i--) {

        // If the ith bit of K is equal
        // to the ith bit of N+1 then the
        // ith bit of X will remain 0
        if ((K >> i & 1) == ((N + 1)
                                 >> i
                             & 1))
            continue;

        // If the ith bit of K is equal to 0
        // and the ith bit of N+1 is equal to 1,
        // set the ith bit of X to 1
        else if ((K >> i & 1) == 0)
            X = X | (1 << i);

        // If the ith bit of K is equal to 1
        // and the ith bit of N+1 is equal to 0,
        // all the remaining bits will
        // remain unset
        else
            break;
    }
    return X;
}

// Driver Code
int main()
{
    // Given Input
    int N = 6, K = 4;
    cout << findMEX(N, K);
    return 0;
}
```

## java 描述语言

```
<script>
    // JavaScript program for the above approach

    // Function to find the MEX of the sequence
    const findMEX = (N, K) => {

        // Calculating the last possible bit
        let lastBit = Math.max(Math.round(Math.log2(N + 1)),
            Math.round(Math.log2(K)));

        // Initialising X
        let X = 0;

        for (let i = lastBit; i >= 0; i--) {

            // If the ith bit of K is equal
            // to the ith bit of N+1 then the
            // ith bit of X will remain 0
            if ((K >> i & 1) == ((N + 1)
                >> i
                & 1))
                continue;

            // If the ith bit of K is equal to 0
            // and the ith bit of N+1 is equal to 1,
            // set the ith bit of X to 1
            else if ((K >> i & 1) == 0)
                X = X | (1 << i);

            // If the ith bit of K is equal to 1
            // and the ith bit of N+1 is equal to 0,
            // all the remaining bits will
            // remain unset
            else
                break;
        }
        return X;
    }

    // Driver Code

    // Given Input
    let N = 6, K = 4;
    document.write(findMEX(N, K));

    // This code is contributed by rakeshsahni

</script>
```

**Output**

```
3
```

***时间复杂度:*** O(log(max(N，K))
***辅助空间:*** O(1)