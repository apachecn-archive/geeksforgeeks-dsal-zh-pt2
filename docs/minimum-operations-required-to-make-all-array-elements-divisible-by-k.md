# 使所有数组元素可被 K 整除所需的最小运算

> 原文:[https://www . geesforgeks . org/minimum-operations-make-all-array-elements-除尽-k/](https://www.geeksforgeeks.org/minimum-operations-required-to-make-all-array-elements-divisible-by-k/)

给定一个**数组 a[]** 、**整数 K** 和一个**整数 X** (初始初始化为 0)。我们的任务是找到更新数组所需的最小移动次数，这样通过执行以下操作，数组中的每个元素都可以被 K 整除:

*   选择一个指数 *i* 从 1 到 N，增加*a<sub>I</sub>T5*X*然后增加*X*1。此操作不能对数组的每个元素应用多次*
*   仅将 X 的值增加 1。

**示例:**

> **输入:** K = 3，a = [1，2，2，18]
> **输出:** 5
> **解释:**
> 最初 X = 0 遂更新 X 为 1。
> 对于 X = 1，将 X 加到数组的第二个元素，使数组[1，3，2，18]增加 X 1。
> 对于 X = 2，将 X 添加到数组[3，3，2，18]的第一个元素，并将 X 增加 1。
> 对于 X = 3，只需将 X 增加 1。
> 对于 X = 4，将 X 加到数组的第三个元素，使数组[3，3，6，18]增加 X 1。
> 最后数组变成[3，3，6，18]其中所有元素都可以被 K = 3 整除。
> **输入:** K = 5，a[] = [15，25，5，10，20，1005，70，80，90，100]
> **输出:** 0
> **解释:**
> 这里所有的元素都已经被 5 整除了。

**方法:**主要思想是找到更新数组元素所需的 X 的最大值，使其能被 k 整除。

*   为此，我们需要找到**的最大值(K –( a<sub>I</sub>mod K)】**来添加数组元素，使其可被 K 整除
*   然而，可以有相等的元素，所以使用**映射**数据结构来跟踪这些元素的数量。
*   当在数组中找到另一个这样的元素时，用**(K –( a<sub>I</sub>mod K))+(K *相等元素的数量)**更新答案，因为每移动一次，我们就增加 X 1。

下面是上述方法的实现:

## C++

```
// C++ implementation to find the
// Minimum number of moves required to
// update the array such that each of
// its element is divisible by K

#include <bits/stdc++.h>
using namespace std;

// Function to find the
// Minimum number of moves required to
// update the array such that each of
// its element is divisible by K
void compute(int a[], int N, int K)
{
    // Initialize Map data structure
    map<long, long> eqVal;

    long maxX = 0;

    // Iterate for all the elements
    // of the array
    for (int i = 0; i < N; i++) {

        // Calculate the
        // value to be added
        long val = a[i] % K;

        val = (val == 0 ? 0 : K - val);

        // Check if the value equals
        // to 0 then simply continue
        if (val == 0)
            continue;

        // Check if the value to be
        // added is present in the map
        if (eqVal.find(val) != eqVal.end()) {

            long numVal = eqVal[val];
            // Update the answer
            maxX = max(maxX,
                    val + (K * numVal));

            eqVal[val]++;
        }

        else {
            eqVal[val]++;
            maxX = max(maxX, val);
        }
    }

    // Print the required result
    // We need to add 1 to maxX
    // because we cant ignore the
    // first move where initially X=0
    // and we need to increase it by 1
    // to make some changes in array
    cout << (maxX == 0 ? 0 : maxX + 1)
        << endl;
}

// Driver code
int main()
{
    int K = 3;
    int a[] = { 1, 2, 2, 18 };
    int N = sizeof(a) / sizeof(a[0]);
    compute(a, N, K);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// minimum number of moves required to
// update the array such that each of
// its element is divisible by K
import java.util.*;

class GFG{

// Function to find the minimum
// number of moves required to
// update the array such that each of
// its element is divisible by K
static void compute(int a[], int N, int K)
{

    // Initialize Map data structure
    Map<Long,
        Long> eqVal = new HashMap<Long,
                                Long>();

    long maxX = 0;

    // Iterate for all the elements
    // of the array
    for(int i = 0; i < N; i++)
    {

        // Calculate the
        // value to be added
        long val = a[i] % K;

        val = (val == 0 ? 0 : K - val);

        // Check if the value equals
        // to 0 then simply continue
        if (val == 0)
            continue;

        // Check if the value to be
        // added is present in the map
        if (eqVal.containsKey(val))
        {
            long numVal = eqVal.get(val);

            // Update the answer
            maxX = Math.max(maxX,
                            val + (K * numVal));

            eqVal.put(val,
            eqVal.getOrDefault(val, 0l) + 1l);
        }
        else
        {
            eqVal.put(val, 1l);
            maxX = Math.max(maxX, val);
        }
    }

    // Print the required result
    // We need to add 1 to maxX
    // because we cant ignore the
    // first move where initially X=0
    // and we need to increase it by 1
    // to make some changes in array
    System.out.println(maxX == 0 ? 0 : maxX + 1);
}

// Driver code
public static void main(String[] args)
{
    int K = 3;
    int a[] = { 1, 2, 2, 18 };
    int N = a.length;

    compute(a, N, K);
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 implementation to find the
# Minimum number of moves required to
# update the array such that each of
# its element is divisible by K
from collections import defaultdict

# Function to find the Minimum number
# of moves required to update the
# array such that each of its
# element is divisible by K
def compute(a, N, K):

    # Initialize Map data structure
    eqVal = defaultdict(int)

    maxX = 0

    # Iterate for all the elements
    # of the array
    for i in range(N):

        # Calculate the
        # value to be added
        val = a[i] % K

        if (val != 0):
            val = K - val

        # Check if the value equals
        # to 0 then simply continue
        if (val == 0):
            continue

        # Check if the value to be
        # added is present in the map
        if (val in eqVal):
            numVal = eqVal[val]

            # Update the answer
            maxX = max(maxX,
                    val + (K * numVal))

            eqVal[val] += 1
        else:
            eqVal[val] += 1
            maxX = max(maxX, val)

    # Print the required result
    # We need to add 1 to maxX
    # because we cant ignore the
    # first move where initially X=0
    # and we need to increase it by 1
    # to make some changes in array
    if maxX == 0:
        print(0)
    else:
        print(maxX + 1)

# Driver code
if __name__ == "__main__":

    K = 3
    a = [ 1, 2, 2, 18 ]
    N = len(a)

    compute(a, N, K)

# This code is contributed by chitranayal
```

## C#

```
// C# implementation to find the
// minimum number of moves required to
// update the array such that each of
// its element is divisible by K
using System;
using System.Collections.Generic;

class GFG{

// Function to find the minimum
// number of moves required to
// update the array such that each of
// its element is divisible by K
static void compute(int []a, int N, int K)
{

    // Initialize Map data structure
    Dictionary<long,
               long> eqVal = new Dictionary<long,
                                            long>();

    long maxX = 0;

    // Iterate for all the elements
    // of the array
    for(int i = 0; i < N; i++)
    {

        // Calculate the
        // value to be added
        long val = a[i] % K;

        val = (val == 0 ? 0 : K - val);

        // Check if the value equals
        // to 0 then simply continue
        if (val == 0)
            continue;

        // Check if the value to be
        // added is present in the map
        if (eqVal.ContainsKey(val))
        {
            long numVal = eqVal[val];

            // Update the answer
            maxX = Math.Max(maxX,
                            val + (K * numVal));

            eqVal[val] = 1 +
            eqVal.GetValueOrDefault(val, 0);
        }
        else
        {
            eqVal.Add(val, 1);
            maxX = Math.Max(maxX, val);
        }
    }

    // Print the required result
    // We need to add 1 to maxX
    // because we cant ignore the
    // first move where initially X=0
    // and we need to increase it by 1
    // to make some changes in array
    Console.Write(maxX == 0 ? 0 : maxX + 1);
}

// Driver code
public static void Main(string[] args)
{
    int K = 3;
    int []a = { 1, 2, 2, 18 };
    int N = a.Length;

    compute(a, N, K);
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

// Javascript implementation to find the
// minimum number of moves required to
// update the array such that each of
// its element is divisible by K

 // Function to find the minimum
// number of moves required to
// update the array such that each of
// its element is divisible by K
    function compute(a,N,K)
    {
        // Initialize Map data structure
    let eqVal = new Map();

    let maxX = 0;

    // Iterate for all the elements
    // of the array
    for(let i = 0; i < N; i++)
    {

        // Calculate the
        // value to be added
        let val = a[i] % K;

        val = (val == 0 ? 0 : K - val);

        // Check if the value equals
        // to 0 then simply continue
        if (val == 0)
            continue;

        // Check if the value to be
        // added is present in the map
        if (eqVal.has(val))
        {
            let numVal = eqVal.get(val);

            // Update the answer
            maxX = Math.max(maxX,
                            val + (K * numVal));

            eqVal.set(val,eqVal.get(val) + 1);
        }
        else
        {
            eqVal.set(val, 1);
            maxX = Math.max(maxX, val);
        }
    }

    // Print the required result
    // We need to add 1 to maxX
    // because we cant ignore the
    // first move where initially X=0
    // and we need to increase it by 1
    // to make some changes in array
    document.write(maxX == 0 ? 0 : maxX + 1);
    }

    // Driver code
    let K = 3;
    let a=[1, 2, 2, 18];
    let N = a.length;
    compute(a, N, K);

// This code is contributed by avanitrachhadiya2155

</script>
```

**Output:** 

```
5
```

***时间复杂度:**O(N)*T4】