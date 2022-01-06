# 数组中不属于递增或递减子序列的最小元素数

> 原文:[https://www . geeksforgeeks . org/数组中非递增或递减子序列的最小元素数/](https://www.geeksforgeeks.org/minimum-number-of-elements-which-are-not-part-of-increasing-or-decreasing-subsequence-in-array/)

给定一组 **n 个**元素。从数组中创建严格递增和严格递减的子序列，使得每个数组元素都属于递增子序列或递减子序列，但不能同时属于这两个子序列，或者可以不属于任何子序列。最小化不属于任何子序列的元素的数量，并计算这些元素的数量。

**示例:**

```
Input : arr[] = { 7, 8, 1, 2, 4, 6, 3, 5, 2, 1, 8, 7 }
Output : 2
Increasing sequence can be { 1, 2, 4, 5, 8 }.
Decreasing sequence can be { 7, 6, 3, 2, 1 }.
So, only 2 (8, 7) element is left which are not part of
either of the subsequences.

Input : arr[] = { 1, 4, 2, 3, 3, 2, 4, 1 }
Output : 0
Increasing sequence can be { 1, 2, 3, 4 }.
Decreasing sequence can be { 4, 3, 2, 1 }.
So, no element is left which is not part of either of 
the subsequences.

```

这个想法是从索引 0 开始，一个接一个地对每个索引做出决定。对于每个指标可以有三种可能，第一，它可以属于递增序列，第二，它可以属于递减序列，第三，它不属于这些序列中的任何一个。
因此，对于每个索引，通过将其视为递增子序列的一部分或递减子序列的一部分来检查最佳答案(不属于任何子序列的最小元素)。如果他们不能得到最佳答案，那么就让它作为不属于任何序列的元素。

为了降低复杂性(使用动态规划)，我们可以使用 3D 数组 dp[x][y][z]存储不属于任何子序列的元素数量，其中 x 表示决策索引，y 表示递减序列的最后一个索引，z 表示递增序列的最后一个索引。

以下是该方法的实现:

## C++

```
// C++ program to return minimum number of elements which
// are not part of increasing or decreasing subsequences.
#include<bits/stdc++.h>
#define MAX 102
using namespace std;

// Return minimum number of elements which is not part of
// any of the sequence.
int countMin(int arr[], int dp[MAX][MAX][MAX], int n, int dec,
                                            int inc, int i)
{
    // If already calculated, return value.
    if (dp[dec][inc][i] != -1)
        return dp[dec][inc][i];

    // If whole array is traversed.
    if (i == n)
        return 0;

    // calculating by considering element as part of
    // decreasing sequence.
    if (arr[i] < arr[dec])
        dp[dec][inc][i] = countMin(arr, dp, n, i, inc, i + 1);

    // calculating by considering element as part of
    // increasing sequence.
    if (arr[i] > arr[inc])
    {
        // If cannot be calculated for decreasing sequence.
        if (dp[dec][inc][i] == -1)
            dp[dec][inc][i] = countMin(arr, dp, n, dec, i, i + 1);

        // After considering once by decreasing sequence, now try
        // for increasing sequence.
        else
            dp[dec][inc][i] = min(countMin(arr, dp, n, dec, i, i + 1),
                                                  dp[dec][inc][i]);
    }

    // If element cannot be part of any of the sequence.
    if (dp[dec][inc][i] == -1)
        dp[dec][inc][i] = 1 + countMin(arr, dp, n, dec, inc, i + 1);

    // After considering element as part of increasing and
    // decreasing sequence trying as not part of any of the
    // sequence.
    else
        dp[dec][inc][i] = min(1 + countMin(arr, dp, n, dec, inc, i + 1),
                                                    dp[dec][inc][i]);

    return dp[dec][inc][i];
}

// Wrapper Function
int wrapper(int arr[], int n)
{
    // Adding two number at the end of array, so that
    // increasing and decreasing sequence can be made.
    // MAX - 2 index is assigned INT_MAX for decreasing sequence
    // because/ next number of sequence must be less than it.
    // Similarly, for Increasing sequence INT_MIN is assigned to
    // MAX - 1 index.
    arr[MAX - 2] = INT_MAX;
    arr[MAX - 1] = INT_MIN;

    int dp[MAX][MAX][MAX];
    memset(dp, -1, sizeof dp);

    return countMin(arr, dp, n, MAX - 2, MAX - 1, 0);
}

// Driven Program
int main()
{
    int n = 12;
    int arr[MAX] = { 7, 8, 1, 2, 4, 6, 3, 5, 2, 1, 8, 7 };

    cout << wrapper(arr, n) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to return minimum number of 
// elements which are not part of increasing
// or decreasing subsequences.
import java.util.*;

class GFG
{

static int MAX = 102;

// Return minimum number of elements which is 
// not part of any of the sequence.
static int countMin(int arr[], int dp[][][], int n,
                    int dec, int inc, int i)
{
    // If already calculated, return value.
    if (dp[dec][inc][i] != -1)
        return dp[dec][inc][i];

    // If whole array is traversed.
    if (i == n)
        return 0;

    // calculating by considering element as 
    // part of decreasing sequence.
    if (arr[i] < arr[dec])
        dp[dec][inc][i] = countMin(arr, dp, n, i, 
                                     inc, i + 1);

    // calculating by considering element as 
    // part of increasing sequence.
    if (arr[i] > arr[inc])
    {
        // If cannot be calculated for 
        // decreasing sequence.
        if (dp[dec][inc][i] == -1)
            dp[dec][inc][i] = countMin(arr, dp, n,
                                       dec, i, i + 1);

        // After considering once by decreasing sequence, 
        // now try for increasing sequence.
        else
            dp[dec][inc][i] = Math.min(countMin(arr, dp, n,
                                                dec, i, i + 1),
                                                dp[dec][inc][i]);
    }

    // If element cannot be part of any of the sequence.
    if (dp[dec][inc][i] == -1)
        dp[dec][inc][i] = 1 + countMin(arr, dp, n, 
                                       dec, inc, i + 1);

    // After considering element as part of increasing and
    // decreasing sequence trying as not part of any of the
    // sequence.
    else
        dp[dec][inc][i] = Math.min(1 + countMin(arr, dp, n,     
                                                dec, inc, i + 1),
                                                dp[dec][inc][i]);

    return dp[dec][inc][i];
}

// Wrapper Function
static int wrapper(int arr[], int n)
{
    // Adding two number at the end of array, 
    // so that increasing and decreasing sequence 
    // can be made. MAX - 2 index is assigned 
    // INT_MAX for decreasing sequence because
    // next number of sequence must be less than it.
    // Similarly, for Increasing sequence INT_MIN 
    // is assigned to MAX - 1 index.
    arr[MAX - 2] = Integer.MAX_VALUE;
    arr[MAX - 1] = Integer.MIN_VALUE;

    int [][][]dp = new int[MAX][MAX][MAX];
    for(int i = 0; i < MAX; i++)
    {
        for(int j = 0; j < MAX; j++)
        {
            for(int l = 0; l < MAX; l++)
            dp[i][j][l] = -1;
        }
    }

    return countMin(arr, dp, n, MAX - 2, 
                                MAX - 1, 0);
}

// Driver Code
public static void main(String[] args) 
{
    int n = 12; 
    int[] arr = new int[MAX];
    arr[0] = 7;
    arr[1] = 8;
    arr[2] = 1;
    arr[3] = 2;
    arr[4] = 4;
    arr[5] = 6;
    arr[6] = 3;
    arr[7] = 5;
    arr[8] = 2;
    arr[9] = 1;
    arr[10] = 8;
    arr[11] = 7; 

    System.out.println(wrapper(arr, n));
}
} 

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to return minimum number of elements which 
# are not part of increasing or decreasing subsequences. 
MAX=102

# Return minimum number of elements which is not part of 
# any of the sequence. 

def countMin(arr,dp,n,dec,inc,i):

    # If already calculated, return value.
    if dp[dec][inc][i] != -1:
        return dp[dec][inc][i]

    # If whole array is traversed. 
    if i==n:
        return 0

    # calculating by considering element as part of 
    # decreasing sequence. 
    if arr[i]<arr[dec]:
        dp[dec][inc][i] = countMin(arr, dp, n, i, inc, i + 1)

    # calculating by considering 
    # element as part of 
    # increasing sequence.
    if arr[i] > arr[inc]:

        # If cannot be calculated for 
        # decreasing sequence.
        if dp[dec][inc][i] == -1:
            dp[dec][inc][i] = countMin(arr, dp, n, dec, i, i + 1)

        # After considering once by 
        # decreasing sequence, now try
        # for increasing sequence. 
        else:
            dp[dec][inc][i] = min(countMin(arr,dp,n,dec,i,i+1),dp[dec][inc][i])

    # If element cannot be part 
    # of any of the sequence.
    if dp[dec][inc][i] == -1:
        dp[dec][inc][i] = 1 + countMin(arr, dp, n, dec, inc, i + 1)

    # After considering element as part of increasing and 
    # decreasing sequence trying as not part of any of the
    # sequence. 
    else:
        dp[dec][inc][i]=min(1+countMin(arr,dp,n,dec,inc,i+1),dp[dec][inc][i])

    return dp[dec][inc][i]

# Wrapper Function
def wrapper(arr,n) :

    # Adding two number at the end of array, so that 
    # increasing and decreasing sequence can be made.
    # MAX - 2 index is assigned INT_MAX for decreasing sequence 
    # because/ next number of sequence must be less than it. 
    # Similarly, for Increasing sequence INT_MIN is assigned to 
    # MAX - 1 index.
    arr[MAX-2]=1000000000
    arr[MAX-1]=-1000000000
    dp=[[[-1 for i in range(MAX)] for i in range(MAX)] for i in range(MAX)]
    return countMin(arr,dp,n,MAX-2,MAX-1,0)

# Driver code
if __name__=='__main__':
    n=12
    arr=[ 7, 8, 1, 2, 4, 6, 3, 5, 2, 1, 8, 7]
    for i in range(MAX):
        arr.append(0)
    print(wrapper(arr,n))

# This code is contributed by sahilshelangia
```

## C#

```
// C# program to return minimum number of
// elements which are not part of increasing
// or decreasing subsequences. 
using System; 

class GFG 
{ 
static int MAX = 102; 

// Return minimum number of elements 
// which is not part of any of the sequence. 
static int countMin(int[] arr, int[,,] dp, int n,   
                    int dec, int inc, int i) 
{ 
    // If already calculated, return value. 
    if (dp[dec, inc, i] != -1) 
        return dp[dec, inc, i]; 

    // If whole array is traversed. 
    if (i == n) 
        return 0; 

    // calculating by considering element 
    // as part of decreasing sequence. 
    if (arr[i] < arr[dec]) 
        dp[dec, inc, i] = countMin(arr, dp, n, i,
                                        inc, i + 1); 

    // calculating by considering element 
    // as part of increasing sequence. 
    if (arr[i] > arr[inc]) 
    { 
        // If cannot be calculated for 
        // decreasing sequence. 
        if (dp[dec, inc, i] == -1) 
            dp[dec, inc, i] = countMin(arr, dp, n,
                                       dec, i, i + 1); 

        // After considering once by decreasing 
        // sequence, now try for increasing sequence. 
        else
            dp[dec, inc, i] = Math.Min(countMin(arr, dp, n, 
                                                dec, i, i + 1), 
                                                dp[dec, inc, i]); 
    } 

    // If element cannot be part of any of the sequence. 
    if (dp[dec, inc, i] == -1) 
        dp[dec, inc, i] = 1 + countMin(arr, dp, n, dec, 
                                            inc, i + 1); 

    // After considering element as part of 
    // increasing and decreasing sequence
    // trying as not part of any of the 
    // sequence. 
    else
        dp[dec, inc, i] = Math.Min(1 + countMin(arr, dp, n, 
                                                dec, inc, i + 1), 
                                                dp[dec, inc, i]); 

    return dp[dec, inc, i]; 
} 

// Wrapper Function 
static int wrapper(int[] arr, int n) 
{ 
    // Adding two number at the end of array, 
    // so that increasing and decreasing sequence 
    // can be made. MAX - 2 index is assigned
    // INT_MAX for decreasing sequence because next 
    // number of sequence must be less than it. 
    // Similarly, for Increasing sequence INT_MIN 
    // is assigned to MAX - 1 index. 
    arr[MAX - 2] = int.MaxValue; 
    arr[MAX - 1] = int.MinValue; 

    int[,,] dp = new int[MAX, MAX, MAX]; 
    for(int i = 0; i < MAX; i++)
        for(int j = 0; j < MAX; j++)
            for(int k = 0; k < MAX; k++)
                dp[i, j, k] = -1;

    return countMin(arr, dp, n, MAX - 2, 
                                MAX - 1, 0); 
} 

// Driver Code
static void Main() 
{ 
    int n = 12; 
    int[] arr = new int[MAX];
    arr[0] = 7;
    arr[1] = 8;
    arr[2] = 1;
    arr[3] = 2;
    arr[4] = 4;
    arr[5] = 6;
    arr[6] = 3;
    arr[7] = 5;
    arr[8] = 2;
    arr[9] = 1;
    arr[10] = 8;
    arr[11] = 7; 

    Console.Write(wrapper(arr, n));
}
}

// This code is contributed by DrRoot_
```

**Output:**

```
2

```

**时间复杂度:** O(n <sup>3</sup>

本文由 ****Anuj Chauhan**** 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。