# 具有相同设置位数的数组中的对的计数

> 原文:[https://www . geeksforgeeks . org/具有相同设置位数的阵列中对的计数/](https://www.geeksforgeeks.org/count-of-pairs-in-an-array-with-same-number-of-set-bits/)

给定一个包含 **N** 整数的数组 **arr** ，任务是计算具有相同设置位数的元素对的可能数量。

**示例:**

> **输入:** N = 8，arr[] = {1，2，3，4，5，6，7，8}
> **输出:** 9
> **解释:**
> 1 组位的元素:1，2，4，8
> 2 组位的元素:3，5，6
> 3 组位的元素:7
> 因此，{1，2}，{1，4}，{1，8}，{2，4}
> 
> **输入:** N = 12，arr[] = {1，2，3，4，5，6，7，8，9，10，11，12}
> **输出:** 22

**进场:**

*   预计算并存储所有数字的设置位，直到**位计数[]** 中数组的最大元素。对于 2 的所有幂，将 1 存储在它们各自的索引处。之后，通过以下关系计算剩余元素的设置位数:

> bits count[I]= bits count[先前 2 的幂]+bits count[I–先前 2 的幂]

*   将数组元素中设置位的频率存储在[映射](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)中。
*   为每个设置的位计数添加可能的对的数量。如果 X 个元素具有相同数量的设置位，它们之间可能的对的数量是**X *(X–1)/2**。
*   打印此类对的总数。

下面的代码是上述方法的实现:

## C++14

```
// C++ Program to count
// possible number of pairs
// of elements with same
// number of set bits.

#include <bits/stdc++.h>
using namespace std;

// Function to return the
// count of Pairs
int countPairs(int arr[], int N)
{
    // Get the maximum element
    int maxm = *max_element(arr, arr + N);

    int i, k;
    // Array to store count of bits
    // of all elements upto maxm
    int bitscount[maxm + 1] = { 0 };

    // Store the set bits
    // for powers of 2
    for (i = 1; i <= maxm; i *= 2)
        bitscount[i] = 1;
    // Compute the set bits for
    // the remaining elements
    for (i = 1; i <= maxm; i++) {
        if (bitscount[i] == 1)
            k = i;
        if (bitscount[i] == 0) {
            bitscount[i]
                = bitscount[k]
                  + bitscount[i - k];
        }
    }

    // Store the frequency
    // of respective counts
    // of set bits
    map<int, int> setbits;
    for (int i = 0; i < N; i++) {
        setbits[bitscount[arr[i]]]++;
    }

    int ans = 0;
    for (auto it : setbits) {
        ans += it.second
               * (it.second - 1) / 2;
    }

    return ans;
}

int main()
{
    int N = 12;
    int arr[] = { 1, 2, 3, 4, 5, 6, 7,
                  8, 9, 10, 11, 12 };

    cout << countPairs(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count possible
// number of pairs of elements
// with same number of set bits
import java.util.*;
import java.lang.*;

class GFG{

// Function to return the
// count of Pairs
static int countPairs(int []arr, int N)
{

    // Get the maximum element
    int maxm = arr[0];

    for(int j = 1; j < N; j++)
    {
        if (maxm < arr[j])
        {
            maxm = arr[j];
        }
    }

    int i, k = 0;

    // Array to store count of bits
    // of all elements upto maxm
    int[] bitscount = new int[maxm + 1];
    Arrays.fill(bitscount, 0);

    // Store the set bits
    // for powers of 2
    for(i = 1; i <= maxm; i *= 2)
        bitscount[i] = 1;

    // Compute the set bits for
    // the remaining elements
    for(i = 1; i <= maxm; i++)
    {
        if (bitscount[i] == 1)
            k = i;
        if (bitscount[i] == 0)
        {
            bitscount[i] = bitscount[k] + 
                           bitscount[i - k];
        }
    }

    // Store the frequency
    // of respective counts
    // of set bits
    Map<Integer, Integer> setbits = new HashMap<>();

    for(int j = 0; j < N; j++) 
    {
        setbits.put(bitscount[arr[j]],
        setbits.getOrDefault(
            bitscount[arr[j]], 0) + 1);
    }

    int ans = 0;

    for(int it : setbits.values())
    {
        ans += it * (it - 1) / 2;

    }
    return ans;
}

// Driver code
public static void main(String[] args)
{
    int N = 12;
    int []arr = { 1, 2, 3, 4, 5, 6, 7,
                  8, 9, 10, 11, 12 };

    System.out.println(countPairs(arr, N));
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program to count possible number
# of pairs of elements with same number
# of set bits.

# Function to return the
# count of Pairs
def countPairs(arr, N):

    # Get the maximum element
    maxm = max(arr)
    i = 0
    k = 0

    # Array to store count of bits
    # of all elements upto maxm
    bitscount = [0 for i in range(maxm + 1)]

    i = 1

    # Store the set bits
    # for powers of 2
    while i <= maxm:
        bitscount[i] = 1
        i *= 2

    # Compute the set bits for
    # the remaining elements
    for i in range(1, maxm + 1):
        if (bitscount[i] == 1):
            k = i
        if (bitscount[i] == 0):
            bitscount[i] = (bitscount[k] +
                            bitscount[i - k])

    # Store the frequency
    # of respective counts
    # of set bits
    setbits = dict()

    for i in range(N):
        if bitscount[arr[i]] in setbits:
            setbits[bitscount[arr[i]]] += 1
        else:
            setbits[bitscount[arr[i]]] = 1

    ans = 0

    for it in setbits.values():
        ans += it * (it - 1) // 2

    return ans

# Driver Code
if __name__=='__main__':

    N = 12
    arr = [ 1, 2, 3, 4, 5, 6, 7,
            8, 9, 10, 11, 12 ]

    print(countPairs(arr, N))

# This code is contributed by pratham76
```

## C#

```
// C# program to count
// possible number of pairs
// of elements with same
// number of set bits.
using System;
using System.Collections;
using System.Collections.Generic;
using System.Text;

class GFG{

// Function to return the
// count of Pairs
static int countPairs(int []arr, int N)
{

    // Get the maximum element
    int maxm = -int.MaxValue;

    for(int j = 0; j < N; j++)
    {
        if (maxm < arr[j])
        {
            maxm = arr[j];
        }
    }

    int i, k = 0;

    // Array to store count of bits
    // of all elements upto maxm
    int []bitscount = new int[maxm + 1];
    Array.Fill(bitscount, 0);

    // Store the set bits
    // for powers of 2
    for(i = 1; i <= maxm; i *= 2)
        bitscount[i] = 1;

    // Compute the set bits for
    // the remaining elements
    for(i = 1; i <= maxm; i++)
    {
        if (bitscount[i] == 1)
            k = i;
        if (bitscount[i] == 0)
        {
            bitscount[i] = bitscount[k] +
                           bitscount[i - k];
        }
    }

    // Store the frequency
    // of respective counts
    // of set bits
    Dictionary<int,
               int> setbits = new Dictionary<int,
                                             int>();

    for(int j = 0; j < N; j++)
    {
        if (setbits.ContainsKey(bitscount[arr[j]]))
        {
            setbits[bitscount[arr[j]]]++;
        }
        else
        {
            setbits[bitscount[arr[j]]] = 1;
        }
    }

    int ans = 0;

    foreach(KeyValuePair<int, int> it in setbits)
    {
        ans += it.Value * (it.Value - 1) / 2;
    }
    return ans;
}

// Driver Code
public static void Main(string[] args)
{
    int N = 12;
    int []arr = { 1, 2, 3, 4, 5, 6, 7,
                  8, 9, 10, 11, 12 };

    Console.Write(countPairs(arr, N));
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

// Javascript Program to count
// possible number of pairs
// of elements with same
// number of set bits.

// Function to return the
// count of Pairs
function countPairs(arr, N)
{
    // Get the maximum element
    var maxm = arr.reduce((a,b)=>Math.max(a,b));

    var i, k;
    // Array to store count of bits
    // of all elements upto maxm
    var bitscount = Array(maxm+1).fill(0);

    // Store the set bits
    // for powers of 2
    for (i = 1; i <= maxm; i *= 2)
        bitscount[i] = 1;
    // Compute the set bits for
    // the remaining elements
    for (i = 1; i <= maxm; i++) {
        if (bitscount[i] == 1)
            k = i;
        if (bitscount[i] == 0) {
            bitscount[i]
                = bitscount[k]
                  + bitscount[i - k];
        }
    }

    // Store the frequency
    // of respective counts
    // of set bits
    var setbits = new Map();
    for (var i = 0; i < N; i++) {

        if(setbits.has(bitscount[arr[i]]))
            setbits.set(bitscount[arr[i]],
             setbits.get(bitscount[arr[i]])+1)
        else
            setbits.set(bitscount[arr[i]], 1)
    }

    var ans = 0;

    setbits.forEach((value, key) => {
        ans += value
               * (value - 1) / 2;
    });

    return ans;
}

var N = 12;
var arr = [1, 2, 3, 4, 5, 6, 7,
              8, 9, 10, 11, 12];
document.write( countPairs(arr, N));

</script>
```

**Output:** 

```
22
```