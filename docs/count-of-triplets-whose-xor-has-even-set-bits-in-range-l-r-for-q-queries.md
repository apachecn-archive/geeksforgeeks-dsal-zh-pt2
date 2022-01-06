# 三元组的计数，对于 Q 查询

，三元组的异或运算已经在范围[L，R]内设置了偶数位

> 原文:[https://www . geeksforgeeks . org/三胞胎计数-其-xor-具有-偶集-范围内-位-l-r-for-q-query/](https://www.geeksforgeeks.org/count-of-triplets-whose-xor-has-even-set-bits-in-range-l-r-for-q-queries/)

给定大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，以及由类型为 **{L，R}** 的 **M** 查询组成的数组**Q【】**，任务是为每个 **M 打印三元组的计数，该三元组的[异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)在**【L，R】**范围内具有偶数个[设置位](https://www.geeksforgeeks.org/count-set-bits-in-an-integer/)**

**示例:**

> **输入:** arr[] = {1，2，3，4，5}，N = 5，Q[] = {{1，4}，{3，4}}，M = 2
> T3】输出:3
> 0
> T7】解释:
> 执行如下查询:
> 
> 1.  查询(1，4):打印 3。xor 具有偶数个设置位的三元组是{1，2，3}、{1，3，4}和{2，3，4}。
> 2.  查询(3，4):打印 0。没有满足条件的三胞胎。
> 
> **输入:** arr[] = {3，3，3}，N = 2，Q[] = {{1，3}}，M = 1
> **输出:** 1

**方法:**给定的问题可以基于以下观察来解决:

1.  两个数字 **X** 和 **Y** 的[异或](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/),即 **X^Y** 可以有一个<u>偶数</u>的[设定位](https://www.geeksforgeeks.org/count-set-bits-in-an-integer/),条件是:
    1.  **X** 和 **Y** 都有一个 **<u>偶数</u>的设定位数**。
    2.  **X** 和 **Y** 都有一个 **<u>奇数</u>的设定位数**。
2.  因此，只有三个数字的[异或](https://www.geeksforgeeks.org/calculate-xor-1-n/)具有一个 **<u>甚至</u>数量的设定位**的情况，它们是:
    1.  所有三个数字都有一个 **<u>偶数</u>的设定位数**。
    2.  恰好其中两个具有奇数**<u>数量的设定位</u>**<u>，另一个具有偶数<u>数量的设定位。</u></u>
3.  <u><u>因此，通过应用上述观察，可以用[前缀数组](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)的概念来解决该问题。</u></u>

<u><u>按照以下步骤解决问题:</u></u>

*   <u><u>初始化一个大小为 **N+1** 的[前缀数组](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)表示 **preo[]** ，其中 **preo[i]** 存储索引 **i** 之前的元素数量，这些元素具有一个 **<u>奇数</u>数量的设置位**。</u></u>
*   <u><u>创建另一个[前缀数组](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)表示大小为 **N+1** 的 **pree** ，其中**pree【I】**存储索引 **i** 之前的元素数量，这些元素具有 **<u>甚至</u>数量的设置位。**</u></u>
*   <u><u>[遍历数组 arr[]](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) ，并执行以下操作:

    *   使用[**_ _ builtin _ popcount()**](https://www.geeksforgeeks.org/builtin-functions-gcc-compiler/)**函数计算**当前元素中的设置位数。****
    *   **如果设定位数为<u>奇数</u>，则增加**preo【I】****
    *   **否则，递增 **pree[i]****</u></u> 
*   <u><u>**[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **Q[]** 并执行以下步骤:

    *   使用**preo【】**数组计算具有 **<u>奇数</u>设定位数**的元素数量，并将其存储在变量中，比如**奇数、**。
    *   使用**pree【】**数组计算具有 **<u>偶数</u>设定位数**的元素数量，并将其存储在变量中，比如**偶数、**。
    *   将变量**和**初始化为 **0** 来存储三胞胎的数量。
    *   如果**连**不小于 **3** ，则在 **ans** 上加上**T5】连 C<sub>3</sub>T9】。**
    *   若**偶数**不小于 **1** 、**奇数**不小于 **2** ，则加 **( <sup>奇数</sup> C <sub>2</sub> )*( <sup>偶数</sup> C <sub>1</sub> )** 至 **ans** 。
    *   最后，打印当前查询 **{L，R}在**和**中获得的三胞胎计数。****</u></u> 

<u><u>**下面是上述方法的一个实现:**</u></u>

## <u><u>**C++**</u></u>

```
<u>**// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Utility function to calculate NCR
int NCR(int N, int R)
{
    if (R > N - R)
        R = N - R;
    int ans = 1;
    for (int i = 1; i <= R; i++) {
        ans *= N - R + i;
        ans /= i;
    }
    return ans;
}
// Function to answer queries about
// the number of triplets  in range
// whose XOR has an even number of
// set bits
void solveXorTriplets(int arr[], int N,
                      vector<pair<int, int> > Q, int M)
{
    // Prefix arrays to store
    // number that have odd
    // and even setbits
    int preo[N + 1] = { 0 };
    int pree[N + 1] = { 0 };

    // Traverse the array arr[]
    for (int i = 0; i < N; i++) {
        // Update
        preo[i + 1] += preo[i];
        pree[i + 1] += pree[i];

        // Find bits in current
        // element
        int setbits = __builtin_popcount(arr[i]);

        // If number of setbits
        // is odd
        if (setbits % 2)
            preo[i + 1]++;
        // Otherwise
        else
            pree[i + 1]++;
    }
    // Traverse the query Q[][]
    for (int i = 0; i < M; i++) {
        // Stores Left boundary
        int L = Q[i].first;
        // Stores Right boundary
        int R = Q[i].second;

        // Stores number of elements
        // that have odd set bits in
        // the given range
        int odd = preo[R] - preo[L - 1];

        // Store number of elements
        // that have even set bits
        // in given range
        int even = pree[R] - pree[L - 1];

        // Store the count
        // of the triplets
        int ans = 0;

        // If even is greater
        // than ore equal to 3
        if (even >= 3)
            ans += NCR(even, 3);

        // If odd is greater than
        // or equal to and even is
        // greater than or equal to
        // 1
        if (odd >= 2 && even >= 1)
            ans += NCR(odd, 2) * NCR(even, 1);

        // Print the answer
        // for current query
        cout << ans << endl;
    }
}
// Driver Code
int main()
{

    int arr[] = { 1, 2, 3, 4, 5 };
    int N = sizeof(arr) / sizeof(arr[0]);

    vector<pair<int, int> > Q = { { 1, 4 }, { 3, 4 } };
    int M = Q.size();

    solveXorTriplets(arr, N, Q, M);
    return 0;
}**</u>
```

## <u><u>**Java 语言(一种计算机语言，尤用于创建网站)**</u></u>

```
<u>**// Java program for the above approach
import java.io.*;
import java.lang.*;
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

// Utility function to calculate NCR
static int NCR(int N, int R)
{
    if (R > N - R)
        R = N - R;

    int ans = 1;

    for(int i = 1; i <= R; i++)
    {
        ans *= N - R + i;
        ans /= i;
    }
    return ans;
}

// Function to answer queries about
// the number of triplets  in range
// whose XOR has an even number of
// set bits
static void solveXorTriplets(int arr[], int N,
                             Vector<pair> Q, int M)
{

    // Prefix arrays to store
    // number that have odd
    // and even setbits
    int preo[] = new int[N + 1];
    int pree[] = new int[N + 1];

    // Traverse the array arr[]
    for(int i = 0; i < N; i++)
    {

        // Update
        preo[i + 1] += preo[i];
        pree[i + 1] += pree[i];

        // Find bits in current
        // element
        int setbits = Integer.bitCount(arr[i]);

        // If number of setbits
        // is odd
        if (setbits % 2 != 0)
            preo[i + 1]++;

        // Otherwise
        else
            pree[i + 1]++;
    }

    // Traverse the query Q[][]
    for(int i = 0; i < M; i++)
    {

        // Stores Left boundary
        int L = Q.elementAt(i).first;

        // Stores Right boundary
        int R =  Q.elementAt(i).second;

        // Stores number of elements
        // that have odd set bits in
        // the given range
        int odd = preo[R] - preo[L - 1];

        // Store number of elements
        // that have even set bits
        // in given range
        int even = pree[R] - pree[L - 1];

        // Store the count
        // of the triplets
        int ans = 0;

        // If even is greater
        // than ore equal to 3
        if (even >= 3)
            ans += NCR(even, 3);

        // If odd is greater than
        // or equal to and even is
        // greater than or equal to
        // 1
        if (odd >= 2 && even >= 1)
            ans += NCR(odd, 2) * NCR(even, 1);

        // Print the answer
        // for current query
        System.out.println(ans);
    }
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 1, 2, 3, 4, 5 };
    int N = arr.length;

    Vector<pair> Q = new Vector<>();
      Q.add(new pair(1, 4));
      Q.add(new pair(3, 4));

    int M = Q.size();

    solveXorTriplets(arr, N, Q, M);
}
}

// This code is contributed by Dharanendra L V.**</u>
```

## <u><u>**蟒蛇 3**</u></u>

```
<u>**# Python3 program for the above approach

# Utility function to calculate NCR
def NCR(N, R):
    if (R > N - R):
        R = N - R
    ans = 1
    for i in range(1,R+1):
        ans *= N - R + i
        ans //= i
    return ans

# Function to answer queries about
# the number of triplets  in range
# whose XOR has an even number of
# set bits
def solveXorTriplets(arr, N, Q, M):
    # Prefix arrays to store
    # number that have odd
    # and even setbits
    preo = [0]*(N + 1)
    pree = [0]*(N + 1)

    # Traverse the array arr[]
    for i in range(N):
        preo[i + 1] += preo[i]
        pree[i + 1] += pree[i]

        # Find bits in current
        # element
        setbits =bin(arr[i]).count('1')

        # If number of setbits
        # is odd
        if (setbits % 2):
            preo[i + 1] +=1
        # Otherwise
        else:
            pree[i + 1]+=1

    # Traverse the query Q[][]
    for i in range(M):

        # Stores Left boundary
        L = Q[i][0]

        # Stores Right boundary
        R = Q[i][1]

        # Stores number of elements
        # that have odd set bits in
        # the given range
        odd = preo[R] - preo[L - 1]

        # Store number of elements
        # that have even set bits
        # in given range
        even = pree[R] - pree[L - 1]

        # Store the count
        # of the triplets
        ans = 0

        # If even is greater
        # than ore equal to 3
        if (even >= 3):
            ans += NCR(even, 3)

        # If odd is greater than
        # or equal to and even is
        # greater than or equal to
        # 1
        if (odd >= 2 and even >= 1):
            ans += NCR(odd, 2) * NCR(even, 1)

        # Print answer
        # for current query
        print (ans)

# Driver Code
if __name__ == '__main__':

    arr = [1, 2, 3, 4, 5]
    N = len(arr)

    Q = [ [ 1, 4 ], [ 3, 4 ] ]
    M = len(Q)

    solveXorTriplets(arr, N, Q, M)

# This code is contributed by mohit kumar 29.**</u>
```

## <u><u>**C#**</u></u>

```
<u>**// C# program for the above approach
using System;
using System.Collections.Generic;

class pair{

    int first, second;

    pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }  

    public static int BitCount(int n)
    {
        var count = 0;
        while (n != 0)
        {
            count++;
            n &= (n - 1); //walking through all the bits which are set to one
        }

        return count;
    }

    // Utility function to calculate NCR
    static int NCR(int N, int R)
    {
        if (R > N - R)
            R = N - R;

        int ans = 1;

        for(int i = 1; i <= R; i++)
        {
            ans *= N - R + i;
            ans /= i;
        }
        return ans;
    }

    // Function to answer queries about
    // the number of triplets  in range
    // whose XOR has an even number of
    // set bits
    static void solveXorTriplets(int[] arr, int N,
                                 List<pair> Q, int M)
    {

        // Prefix arrays to store
        // number that have odd
        // and even setbits
        int[] preo = new int[N + 1];
        int[] pree = new int[N + 1];

        // Traverse the array arr[]
        for(int i = 0; i < N; i++)
        {

            // Update
            preo[i + 1] += preo[i];
            pree[i + 1] += pree[i];

            // Find bits in current
            // element
            int setbits = BitCount(arr[i]);

            // If number of setbits
            // is odd
            if (setbits % 2 != 0)
                preo[i + 1]++;

            // Otherwise
            else
                pree[i + 1]++;
        }

        // Traverse the query Q[][]
        for(int i = 0; i < M; i++)
        {

            // Stores Left boundary
            int L = Q[i].first;

            // Stores Right boundary
            int R =  Q[i].second;

            // Stores number of elements
            // that have odd set bits in
            // the given range
            int odd = preo[R] - preo[L - 1];

            // Store number of elements
            // that have even set bits
            // in given range
            int even = pree[R] - pree[L - 1];

            // Store the count
            // of the triplets
            int ans = 0;

            // If even is greater
            // than ore equal to 3
            if (even >= 3)
                ans += NCR(even, 3);

            // If odd is greater than
            // or equal to and even is
            // greater than or equal to
            // 1
            if (odd >= 2 && even >= 1)
                ans += NCR(odd, 2) * NCR(even, 1);

            // Print the answer
            // for current query
            Console.WriteLine(ans);
        }
    }

    // Driver Code
    public static void Main()
    {
        int[] arr = { 1, 2, 3, 4, 5 };
        int N = arr.Length;

        List<pair> Q = new List<pair>();
          Q.Add(new pair(1, 4));
          Q.Add(new pair(3, 4));

        int M = Q.Count;

        solveXorTriplets(arr, N, Q, M);
    }
}

// This code is contributed by ShubhamSingh10**</u>
```

## <u><u>**C++**</u></u>

```
<u>**#include <iostream>
using namespace std;

int main() {

    cout<<"GFG!";
    return 0;
}**</u>
```

## <u><u>**java 描述语言**</u></u>

```
<u>**<script>

// JavaScript program for the above approach

function bitCount1(n) {
  return n.toString(2).match(/1/g).length
}

// Utility function to calculate NCR
function NCR(N, R)
{
    if (R > N - R)
        R = N - R;
    var ans = 1;
    for (var i = 1; i <= R; i++) {
        ans *= N - R + i;
        ans /= i;
    }
    return ans;
}
// Function to answer queries about
// the number of triplets  in range
// whose XOR has an even number of
// set bits
function solveXorTriplets(arr, N, Q, M)
{
    // Prefix arrays to store
    // number that have odd
    // and even setbits
    var preo = new Array(N+1).fill(0);
    var pree = new Array(N+1).fill(0);

    // Traverse the array arr[]
    for (var i = 0; i < N; i++) {
        // Update
        preo[i + 1] += preo[i];
        pree[i + 1] += pree[i];

        // Find bits in current
        // element
        var setbits = bitCount1(arr[i]);

        // If number of setbits
        // is odd
        if (setbits % 2)
            preo[i + 1]++;
        // Otherwise
        else
            pree[i + 1]++;
    }
    // Traverse the query Q[][]
    for (var i = 0; i < M; i++) {
        // Stores Left boundary
        var L = Q[i][0];
        // Stores Right boundary
        var R = Q[i][1];

        // Stores number of elements
        // that have odd set bits in
        // the given range
        var odd = preo[R] - preo[L - 1];

        // Store number of elements
        // that have even set bits
        // in given range
        var even = pree[R] - pree[L - 1];

        // Store the count
        // of the triplets
        var ans = 0;

        // If even is greater
        // than ore equal to 3
        if (even >= 3)
            ans += NCR(even, 3);

        // If odd is greater than
        // or equal to and even is
        // greater than or equal to
        // 1
        if (odd >= 2 && even >= 1)
            ans += NCR(odd, 2) * NCR(even, 1);

        // Print the answer
        // for current query
        document.write(ans + "<br>");
    }
}
// Driver Code
var arr = [1, 2, 3, 4, 5 ];
var N = arr.length;

var Q = [ [ 1, 4 ], [ 3, 4 ] ];
var M = Q.length;

solveXorTriplets(arr, N, Q, M);

// This code is contributed by Shubhamsingh10

</script>**</u>
```

<u><u>****Output**

```
3
0
```**</u></u> 

<u><u>*****时间复杂度:** O(N+M)*
***辅助空间:** O(N)***</u></u>