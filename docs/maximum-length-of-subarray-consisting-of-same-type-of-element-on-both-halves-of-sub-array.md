# 子阵列的最大长度，由子阵列两半上相同类型的元素组成

> 原文:[https://www . geeksforgeeks . org/子阵列的最大长度-由子阵列的两半上的相同类型的元素组成/](https://www.geeksforgeeks.org/maximum-length-of-subarray-consisting-of-same-type-of-element-on-both-halves-of-sub-array/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是找到子数组的最大长度，该子数组由子数组两半上相同类型的元素组成。此外，两半上的元素彼此不同。

**示例:**

> ***输入:** arr[] = {2，3，4，4，5，5，6，7，8，10}*
> ***输出:** 4*
> ***解释:***
> *{2，3}、{3，4}、{4，4，5，5}、{5，6}等是两个半部分只有一种元素类型的有效子数组。*
> *{4，4，5，5}是长度最大的子阵列。*
> *遂，输出为 4。*
> 
> ***输入:** arr[] = {1，7，7，10，10，7，7，7，8，8，9}*
> ***输出:** 6*
> ***解释:***
> *{1，7}，{7，7，10，10}，{7，7，8，8，8}，{8，9}等是有效的*
> *{7，7，7，8，8，8}是长度最大的子阵列。*
> *遂，输出为 6。*

**天真的做法:**天真的想法是[生成所有可能的子阵列](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)并检查任何具有最大长度的子阵列是否可以分成两半，使得两半中的所有元素都相同。

***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(1)*

**有效方法:**解决这个问题的思路是使用[前缀和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)的概念。按照以下步骤解决问题:

1.  从开始向前遍历数组，并将每个索引的整数连续出现存储在数组**向前[]。**
2.  同样，从数组的末尾开始反向遍历数组，并将每个索引的一个整数的连续出现存储在一个数组中**向后[]** 。
3.  存储 ***min(向前[i]，向后[i+1])*2、*** 的最大值为所有的索引，其中 **arr[i]！=arr[i+1]** 。
4.  打印在上述步骤中获得的值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function that finds the maximum
// length of the sub-array that
// contains equal element on both
// halves of sub-array
void maxLengthSubArray(int A[], int N)
{

    // To store continuous occurence
    // of the element
    int forward[N], backward[N];

    // To store continuous
    // forward occurence
    for (int i = 0; i < N; i++) {

        if (i == 0
            || A[i] != A[i - 1]) {
            forward[i] = 1;
        }
        else
            forward[i] = forward[i - 1] + 1;
    }

    // To store continuous
    // backward occurence
    for (int i = N - 1; i >= 0; i--) {

        if (i == N - 1
            || A[i] != A[i + 1]) {
            backward[i] = 1;
        }
        else
            backward[i] = backward[i + 1] + 1;
    }

    // To store the maximum length
    int ans = 0;

    // Find maximum length
    for (int i = 0; i < N - 1; i++) {

        if (A[i] != A[i + 1])
            ans = max(ans,
                    min(forward[i],
                        backward[i + 1])
                        * 2);
    }

    // Print the result
    cout << ans;
}

// Driver Code
int main()
{
    // Given array
    int arr[] = { 1, 2, 3, 4, 4,
                4, 6, 6, 6, 9 };

    // Size of the array
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    maxLengthSubArray(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach         
class GFG{         

// Function that finds the maximum         
// length of the sub-array that         
// contains equal element on both         
// halves of sub-array         
static void maxLengthSubArray(int A[], int N)         
{

    // To store continuous occurence         
    // of the element         
    int forward[] = new int[N];         
    int backward[] = new int[N];         

    // To store continuous         
    // forkward occurence         
    for(int i = 0; i < N; i++)
    {
        if (i == 0 || A[i] != A[i - 1])
        {         
            forward[i] = 1;         
        }         
        else         
            forward[i] = forward[i - 1] + 1;         
    }         

    // To store continuous         
    // backward occurence         
    for(int i = N - 1; i >= 0; i--)
    {
        if (i == N - 1 || A[i] != A[i + 1])
        {         
            backward[i] = 1;         
        }         
        else         
            backward[i] = backward[i + 1] + 1;         
    }         

    // To store the maximum length         
    int ans = 0;         

    // Find maximum length         
    for(int i = 0; i < N - 1; i++)
    {         
        if (A[i] != A[i + 1])         
            ans = Math.max(ans,         
                           Math.min(forward[i],         
                                    backward[i + 1]) * 2);         
    }         

    // Print the result         
    System.out.println(ans);         
}         

// Driver Code         
public static void main(String[] args)
{         

    // Given array         
    int arr[] = { 1, 2, 3, 4, 4,         
                  4, 6, 6, 6, 9 };         

    // Size of the array         
    int N = arr.length;         

    // Function call         
    maxLengthSubArray(arr, N);         
}         
}

// This code is contributed by rutvik_56
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function that finds the maximum
# length of the sub-array that
# contains equal element on both
# halves of sub-array
def maxLengthSubArray(A, N):

    # To store continuous occurence
    # of the element
    forward = [0] * N
    backward = [0] * N

    # To store continuous
    # forward occurence
    for i in range(N):
            if i == 0 or A[i] != A[i - 1]:
                forward[i] = 1
            else:
                forward[i] = forward[i - 1] + 1

    # To store continuous
    # backward occurence
    for i in range(N - 1, -1, -1):
        if i == N - 1 or A[i] != A[i + 1]:
            backward[i] = 1
        else:
            backward[i] = backward[i + 1] + 1

    # To store the maximum length
    ans = 0

    # Find maximum length
    for i in range(N - 1):
        if (A[i] != A[i + 1]):
            ans = max(ans,
                    min(forward[i],
                        backward[i + 1]) * 2);

    # Print the result
    print(ans)

# Driver Code

# Given array
arr = [ 1, 2, 3, 4, 4, 4, 6, 6, 6, 9 ]

# Size of the array
N = len(arr)

# Function call
maxLengthSubArray(arr, N)

# This code is contributed by yatinagg
```

## C#

```
// C# program for the above approach         
using System;
class GFG{         

// Function that finds the maximum         
// length of the sub-array that         
// contains equal element on both         
// halves of sub-array         
static void maxLengthSubArray(int []A, int N)         
{

    // To store continuous occurence         
    // of the element         
    int []forward = new int[N];         
    int []backward = new int[N];         

    // To store continuous         
    // forkward occurence         
    for(int i = 0; i < N; i++)
    {
        if (i == 0 || A[i] != A[i - 1])
        {         
            forward[i] = 1;         
        }         
        else         
            forward[i] = forward[i - 1] + 1;         
    }         

    // To store continuous         
    // backward occurence         
    for(int i = N - 1; i >= 0; i--)
    {
        if (i == N - 1 || A[i] != A[i + 1])
        {         
            backward[i] = 1;         
        }         
        else         
            backward[i] = backward[i + 1] + 1;         
    }         

    // To store the maximum length         
    int ans = 0;         

    // Find maximum length         
    for(int i = 0; i < N - 1; i++)
    {         
        if (A[i] != A[i + 1])         
            ans = Math.Max(ans,         
                           Math.Min(forward[i],         
                                    backward[i + 1]) * 2);         
    }         

    // Print the result         
    Console.WriteLine(ans);         
}         

// Driver Code         
public static void Main(String[] args)
{         

    // Given array         
    int []arr = { 1, 2, 3, 4, 4,         
                  4, 6, 6, 6, 9 };         

    // Size of the array         
    int N = arr.Length;         

    // Function call         
    maxLengthSubArray(arr, N);         
}         
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function that finds the maximum        
// length of the sub-array that        
// contains equal element on both        
// halves of sub-array        
function maxLengthSubArray(A, N)        
{

    // To store continuous occurence        
    // of the element        
    let forward = Array.from({length: N}, (_, i) => 0);       
    let backward = Array.from({length: N}, (_, i) => 0);   

    // To store continuous        
    // forkward occurence        
    for(let i = 0; i < N; i++)
    {
        if (i == 0 || A[i] != A[i - 1])
        {        
            forward[i] = 1;        
        }        
        else        
            forward[i] = forward[i - 1] + 1;        
    }        

    // To store continuous        
    // backward occurence        
    for(let i = N - 1; i >= 0; i--)
    {
        if (i == N - 1 || A[i] != A[i + 1])
        {        
            backward[i] = 1;        
        }        
        else        
            backward[i] = backward[i + 1] + 1;        
    }        

    // To store the maximum length        
    let ans = 0;        

    // Find maximum length        
    for(let i = 0; i < N - 1; i++)
    {        
        if (A[i] != A[i + 1])        
            ans = Math.max(ans,        
                           Math.min(forward[i],        
                                    backward[i + 1]) * 2);        
    }        

    // Print the result        
    document.write(ans);        
}        

// Driver Code

    // Given array        
    let arr = [ 1, 2, 3, 4, 4,        
                  4, 6, 6, 6, 9 ];        

    // Size of the array        
    let N = arr.length;        

    // Function call        
    maxLengthSubArray(arr, N);

</script>
```

**Output:** 

```
6
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)