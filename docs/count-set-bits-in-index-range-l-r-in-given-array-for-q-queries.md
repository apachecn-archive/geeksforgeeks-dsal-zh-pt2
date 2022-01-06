# 为 Q 查询计算给定数组中索引范围[L，R]中的设置位

> 原文:[https://www . geesforgeks . org/count-set-bit-in-index-range-l-r-in-给定数组-for-q-query/](https://www.geeksforgeeks.org/count-set-bits-in-index-range-l-r-in-given-array-for-q-queries/)

给定一个包含 **N** 整数的数组**arr【】**和一个包含 **Q** 查询的数组 **{L，R}** ，任务是为每个查询计算数组 **arr** 中从 **L** 到 **R** 的设置位总数。

**示例:**

> **输入:** arr[]={1，2，3，4，5，6}，查询[]={{0，2}，{1，1}，{3，5}}
> **输出:**
> 4
> 2
> 5
> **说明:**
> 查询 1 (0，2):元素{1，2，3}分别设置了位{1，1，2}。所以 sum=1+1+2=4
> 查询 1 (1，1):元素{2}已经设置了位{1}。所以 sum=1
> 查询 1 (3，5):元素{4，5，6}分别设置了位{1，2，2}。所以总和=1+2+2=5
> 
> **输入:** arr[]={2，4，3，5，6}，查询[]={{0，1}，{2，4}}
> **输出:**
> 2
> 6

**方法:**要解决这个问题，请按照以下步骤操作:

1.  创建一个向量，比如说**在**上，其中每个 **i <sup>第</sup>T5】元素将表示从**arr【0】**到**arr【I】**的设置位数。**
2.  运行一个从 **i=0 到 i < N** 的循环，在每次迭代中，找到**arr【I】**中的设置位数，说出位并使**onBits【I】= onBits【I-1】+位**。
3.  现在遍历数组查询，对于每个查询 **{L，R}** ，从 **L** 到 **R** 的设置位数是**OnBit[R]-OnBit[L-1]**。
4.  根据以上观察打印答案。

下面是上述方法的实现:

## C++

```
// C++ code for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to return the number
// of set bits from L to R
int setBitsinLtoR(int L, int R,
                  vector<int>& onBits)
{
    if (L == 0) {
        return onBits[R];
    }

    return onBits[R] - onBits[L - 1];
}

// Function to find the number
// of set bits for Q queries
void totalSetBits(vector<int>& arr,
                  vector<pair<int, int> >& queries)
{
    int N = arr.size();
    vector<int> onBits(N, 0);
    onBits[0] = __builtin_popcount(arr[0]);

    for (int i = 1; i < N; ++i) {
        onBits[i]
            = onBits[i - 1]
              + __builtin_popcount(arr[i]);
    }

    // Finding for Q queries
    for (auto x : queries) {
        int L = x.first;
        int R = x.second;

        cout << setBitsinLtoR(L, R, onBits)
             << endl;
    }
}

// Driver Code
int main()
{
    vector<int> arr = { 1, 2, 3, 4, 5, 6 };
    vector<pair<int, int> > queries
        = { { 0, 2 }, { 1, 1 }, { 3, 5 } };

    totalSetBits(arr, queries);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for the above approach
import java.util.*;
class GFG{

static class pair
{
    int first, second;
    public pair(int first, int second) 
    {
        this.first = first;
        this.second = second;
    }   
}

// Function to return the number
// of set bits from L to R
static int setBitsinLtoR(int L, int R,int []onBits)
{
    if (L == 0) {
        return onBits[R];
    }

    return onBits[R] - onBits[L - 1];
}

// Function to find the number
// of set bits for Q queries
static void totalSetBits(int[] arr,
                  pair[] queries)
{
    int N = arr.length;

    int []onBits = new int[N];
    onBits[0] = Integer.bitCount(arr[0]);

    for (int i = 1; i < N; ++i) {
        onBits[i]
            = onBits[i - 1]
              + Integer.bitCount(arr[i]);
    }

    // Finding for Q queries
    for (pair x : queries) {
        int L = x.first;
        int R = x.second;

        System.out.print(setBitsinLtoR(L, R, onBits)
             +"\n");
    }
}

// Driver Code
public static void main(String[] args)
{
    int []arr = { 1, 2, 3, 4, 5, 6 };
    pair []queries
        = { new pair( 0, 2 ), new pair( 1, 1 ), new pair( 3, 5 ) };

    totalSetBits(arr, queries);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python code for the above approach
def  __builtin_popcount(n):
    count = 0
    while (n):
        count += n & 1
        n >>= 1
    return count

# Function to return the number
# of set bits from L to R
def setBitsinLtoR(L, R, onBits):
    if (L == 0):
        return onBits[R];
    return onBits[R] - onBits[L - 1];

# Function to find the number
# of set bits for Q queries
def totalSetBits(arr, queries):
    N = len(arr);
    onBits = [0] * N
    onBits[0] = __builtin_popcount(arr[0]);

    for i in range(1, N):
        onBits[i] = onBits[i - 1] +  __builtin_popcount(arr[i]);

    # Finding for Q queries
    for x in queries:
        L = x[0];
        R = x[1];

        print(setBitsinLtoR(L, R, onBits))

# Driver Code
arr = [ 1, 2, 3, 4, 5, 6 ];
queries = [ [ 0, 2 ], [ 1, 1 ], [ 3, 5 ] ];

totalSetBits(arr, queries);

# This code is contributed by gfgking
```

## C#

```
// C# code for the above approach
using System;

class GFG{

class pair
{
    public int first, second;

    public pair(int first, int second) 
    {
        this.first = first;
        this.second = second;
    }   
}

// Function to return the number
// of set bits from L to R
static int setBitsinLtoR(int L, int R, int []onBits)
{
    if (L == 0)
    {
        return onBits[R];
    }

    return onBits[R] - onBits[L - 1];
}

// Function to find the number
// of set bits for Q queries
static void totalSetBits(int[] arr,
                         pair[] queries)
{
    int N = arr.Length;
    int []onBits = new int[N];
    onBits[0] = bitCount(arr[0]);

    for(int i = 1; i < N; ++i)
    {
        onBits[i] = onBits[i - 1] +
                    bitCount(arr[i]);
    }

    // Finding for Q queries
    foreach (pair x in queries)
    {
        int L = x.first;
        int R = x.second;

        Console.Write(setBitsinLtoR(L, R, onBits) +
                      "\n");
    }
}

static int bitCount(int x)
{
    int setBits = 0;
    while (x != 0)
    {
        x = x & (x - 1);
        setBits++;
    }
    return setBits;
}

// Driver Code
public static void Main(String[] args)
{
    int []arr = { 1, 2, 3, 4, 5, 6 };
    pair []queries = { new pair(0, 2),
                       new pair(1, 1),
                       new pair(3, 5) };

    totalSetBits(arr, queries);
}
}

// This code is contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// JavaScript code for the above approach
function __builtin_popcount(x)
{
    return((x).toString(2).split('').
           filter(x => x == '1').length);
}

// Function to return the number
// of set bits from L to R
function setBitsinLtoR(L, R, onBits)
{
    if (L == 0)
    {
        return onBits[R];
    }
    return onBits[R] - onBits[L - 1];
}

// Function to find the number
// of set bits for Q queries
function totalSetBits(arr, queries)
{
    let N = arr.length;
    let onBits = new Array(N).fill(0);
    onBits[0] = __builtin_popcount(arr[0]);

    for(let i = 1; i < N; ++i)
    {
        onBits[i] = onBits[i - 1] +
                    __builtin_popcount(arr[i]);
    }

    // Finding for Q queries
    for(let x of queries)
    {
        let L = x[0];
        let R = x[1];

        document.write(
            setBitsinLtoR(L, R, onBits) + '<br>')
    }
}

// Driver Code
let arr = [ 1, 2, 3, 4, 5, 6 ];
let queries = [ [ 0, 2 ], [ 1, 1 ], [ 3, 5 ] ];

totalSetBits(arr, queries);

// This code is contributed by Potta Lokesh

</script>
```

**Output**

```
4
1
5
```

**时间复杂度:** O(Q*N*logK)，其中 N 为数组 arr 的大小，Q 为查询数，K 为位数
T3】辅助空间: O(N)