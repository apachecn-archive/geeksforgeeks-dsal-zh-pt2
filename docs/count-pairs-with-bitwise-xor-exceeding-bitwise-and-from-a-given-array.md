# 对给定数组中按位异或超过按位与的对进行计数

> 原文:[https://www . geesforgeks . org/count-pairs-with-bitwise-xor-over-bitwise-and-from-from-给定数组/](https://www.geeksforgeeks.org/count-pairs-with-bitwise-xor-exceeding-bitwise-and-from-a-given-array/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)、**arr【】**，任务是计算给定数组中的对的数量，使得每对的[位 AND( & )](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/) 小于其[位 XOR(^)](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/) 。

**示例:**

> **输入:** arr[] = {1，2，3，4，5}
> **输出:** 11
> **解释:**
> 满足给定条件的对为:
> (1&2)<(1 ^ 2)
> (1&3)<(1 ^ 3)
> (1&4)<(1 ^ 4)
> (1【t22
> 
> **输入:** arr[] = {1，4，3，7，10}
> **输出:** 9

**方法:**最简单的方法是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)和[从给定数组](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)生成所有可能的对。对于每对，检查其按位“与”(&)是否小于该对的按位“XOR(^”)。如果发现为真，则按 **1** 增加对的计数。最后，打印获得的这种对的计数。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**高效方法:**要优化上述方法，请遵循[按位运算符](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/)的属性:

> 1 ^ 0 = 1
> 0 ^ 1 = 1
> 1&1 = 1
> x = b<sub>31</sub>b<sub>30</sub>…..b<sub>1</sub>b<sub>0</sub>
> Y = a<sub>31</sub>b<sub>30</sub>…。a <sub>1</sub> a <sub>0</sub>
> 如果表达式{(X & Y) > (X ^ Y)}为真，则 x 和 y 的最高有效位(MSB)必须相等。
> 满足条件{(X & Y) > (X ^ Y)}的配对总数为:
> 
> ![\sum_{i=0}^{31}\binom{bit[i]}{2}                  ](img/b40aa4c6486964d938c21c4f4d54ccd7.png "Rendered by QuickLaTeX.com")
> 位[i]存储最高有效位(MSB)位置为 I 的数组元素的计数。
> 
> 因此，满足给定条件的配对总数{(X & Y)< (X ^ Y)} 
> =[{ N *(N–1)/2 }–{
> ![ \sum_{i=0}^{31}\binom{bit[i]}{2}                   ](img/c9c6bd26766efab6622590825d93922d.png "Rendered by QuickLaTeX.com")
> }]

按照以下步骤解决问题:

1.  初始化一个变量，比如 **res** ，以存储满足给定条件的对的计数。
2.  [遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)。
3.  存储给定数组中每个元素的最高有效位的位置。
4.  最后，通过上述公式评估结果并打印结果。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count pairs that
// satisfy the above condition.
int cntPairs(int arr[], int N)
{

    // Stores the count
    // of pairs
    int res = 0;

    // Stores the count of array
    // elements having same
    // positions of MSB
    int bit[32] = { 0 };

    // Traverse the array
    for (int i = 0; i < N; i++) {

        // Stores the index of
        // MSB of array elements
        int pos
            = log2(arr[i]);
        bit[pos]++;
    }

    // Calculate number of pairs
    for (int i = 0; i < 32; i++) {
        res += (bit[i]
                * (bit[i] - 1))
               / 2;
    }
    res = (N * (N - 1)) / 2 - res;

    return res;
}

// Driver Code
int main()
{

    int arr[] = { 1, 2, 3, 4, 5, 6 };
    int N = sizeof(arr) / sizeof(arr[0]);
    cout << cntPairs(arr, N);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.io.*;

class GFG{

// Function to count pairs that
// satisfy the above condition.
static int cntPairs(int[] arr, int N)
{

    // Stores the count
    // of pairs
    int res = 0;

    // Stores the count of array
    // elements having same
    // positions of MSB
    int[] bit = new int[32];

    // Traverse the array
    for(int i = 0; i < N; i++)
    {

        // Stores the index of
        // MSB of array elements
        int pos = (int)(Math.log(arr[i]) /
                        Math.log(2));
        bit[pos]++;
    }

    // Calculate number of pairs
    for(int i = 0; i < 32; i++)
    {
        res += (bit[i] * (bit[i] - 1)) / 2;
    }
    res = (N * (N - 1)) / 2 - res;

    return res;
}

// Driver Code
public static void main(String[] args)
{
    int[] arr = { 1, 2, 3, 4, 5, 6 };
    int N = arr.length;

    System.out.println(cntPairs(arr, N));
}
}

// This code is contributed by akhilsaini
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
import math

# Function to count pairs that
# satisfy the above condition.
def cntPairs(arr, N):

    # Stores the count
    # of pairs
    res = 0

    # Stores the count of array
    # elements having same
    # positions of MSB
    bit = [0] * 32

    # Traverse the array
    for i in range(0, N):

        # Stores the index of
        # MSB of array elements
        pos = int(math.log(arr[i], 2))
        bit[pos] = bit[pos] + 1

    # Calculate number of pairs
    for i in range(0, 32):
        res = res + int((bit[i] *
                        (bit[i] - 1)) / 2)

    res = int((N * (N - 1)) / 2 - res)

    return res

# Driver Code
if __name__ == "__main__":

    arr = [ 1, 2, 3, 4, 5, 6 ]
    N = len(arr)

    print(cntPairs(arr, N))

# This code is contributed by akhilsaini
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to count pairs that
// satisfy the above condition.
static int cntPairs(int[] arr, int N)
{

    // Stores the count
    // of pairs
    int res = 0;

    // Stores the count of array
    // elements having same
    // positions of MSB
    int[] bit = new int[32];

    // Traverse the array
    for(int i = 0; i < N; i++)
    {

        // Stores the index of
        // MSB of array elements
        int pos = (int)(Math.Log(arr[i]) /
                        Math.Log(2));
        bit[pos]++;
    }

    // Calculate number of pairs
    for(int i = 0; i < 32; i++)
    {
        res += (bit[i] * (bit[i] - 1)) / 2;
    }
    res = (N * (N - 1)) / 2 - res;

    return res;
}

// Driver Code
public static void Main()
{
    int[] arr = { 1, 2, 3, 4, 5, 6 };
    int N = arr.Length;

    Console.Write(cntPairs(arr, N));
}
}

// This code is contributed by akhilsaini
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach

// Function to count pairs that
// satisfy the above condition.
function cntPairs(arr, N)
{

    // Stores the count
    // of pairs
    let res = 0;

    // Stores the count of array
    // elements having same
    // positions of MSB
    let bit = new Array(32).fill(0);

    // Traverse the array
    for(let i = 0; i < N; i++)
    {

        // Stores the index of
        // MSB of array elements
        let pos = parseInt(Math.log(arr[i]) /
                           Math.log(2));;
        bit[pos]++;
    }

    // Calculate number of pairs
    for(let i = 0; i < 32; i++)
    {
        res += parseInt((bit[i]
                * (bit[i] - 1)) / 2);
    }
    res = parseInt((N * (N - 1)) / 2) - res;

    return res;
}

// Driver Code
let arr = [ 1, 2, 3, 4, 5, 6 ];
let N = arr.length;

document.write(cntPairs(arr, N));

// This code is contributed by subhammahato348.

</script>
```

**Output:** 

```
11
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)

**方法 2 :** 当且仅当最高有效位相等时，按位“与”大于按位“异或”。

*   创建大小为 32 的**位[]** 数组(最大位数)
*   将**和**初始化为 0。
*   我们将从头开始遍历数组，
    *   找到它的最高有效位，说它是 j。
    *   将存储在**位【j】**数组中的值添加到 **ans** 中。(对于当前元素位[j],可以形成若干对)
    *   现在将**位【j】**的值增加 **1** 。
*   现在总对数= **n*(n-1)/2** 。减去**和**。

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

int findCount(int arr[], int N)
{
    // For storing number of pairs
    int ans = 0;

    // For storing count of numbers
    int bits[32] = { 0 };

    // Iterate from 0 to N - 1
    for (int i = 0; i < N; i++) {

        // Find the most significant bit
        int val = log2l(arr[i]);

        ans += bits[val];
        bits[val]++;
    }
    return N * (N - 1) / 2 - ans;
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 1, 2, 3, 4, 5, 6 };

    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    cout << findCount(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.*;
import java.util.*;

class GFG{

static int findCount(int arr[], int N)
{

    // For storing number of pairs
    int ans = 0;

    // For storing count of numbers
    int bits[] = new int[32];

    // Iterate from 0 to N - 1
    for(int i = 0; i < N; i++)
    {

        // Find the most significant bit
        int val = (int)(Math.log(arr[i]) /
                        Math.log(2));

        ans += bits[val];
        bits[val]++;
    }
    return N * (N - 1) / 2 - ans;
}

// Driver Code
public static void main(String[] args)
{

    // Given array arr[]
    int arr[] = { 1, 2, 3, 4, 5, 6 };

    int N = arr.length;

    // Function Call
    System.out.println(findCount(arr, N));
}
}

// This code is contributed by Kingash
```

## 蟒蛇 3

```
# Python3 program for the above approach
import math
def findCount(arr, N):

    # For storing number of pairs
    ans = 0

    # For storing count of numbers
    bits = [0] * 32

    # Iterate from 0 to N - 1
    for i in range(N):

        # Find the most significant bit
        val = int(math.log2(arr[i]))

        ans += bits[val]
        bits[val] += 1
    return (N * (N - 1) // 2 - ans)

# Driver Code
if __name__ == "__main__":

    # Given array arr[]
    arr = [1, 2, 3, 4, 5, 6]

    N = len(arr)

    # Function Call
    print(findCount(arr, N))

    # This code is contributed by ukasp.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

static int findCount(int[] arr, int N)
{

    // For storing number of pairs
    int ans = 0;

    // For storing count of numbers
    int[] bits = new int[32];

    // Iterate from 0 to N - 1
    for(int i = 0; i < N; i++)
    {

        // Find the most significant bit
        int val = (int)(Math.Log(arr[i]) /
                        Math.Log(2));

        ans += bits[val];
        bits[val]++;
    }
    return N * (N - 1) / 2 - ans;
}

// Driver Code
public static void Main()
{

    // Given array arr[]
    int[] arr = { 1, 2, 3, 4, 5, 6 };

    int N = arr.Length;

    // Function Call
    Console.Write(findCount(arr, N));
}
}

// This code is contributed by subhammahato348
```

## java 描述语言

```
<script>

// Javascript program for the above approach
function findCount(arr, N)
{

    // For storing number of pairs
    let ans = 0;

    // For storing count of numbers
    let bits = new Array(32).fill(0);

    // Iterate from 0 to N - 1
    for(let i = 0; i < N; i++)
    {

        // Find the most significant bit
        let val = parseInt(Math.log(arr[i]) /
                           Math.log(2));

        ans += bits[val];
        bits[val]++;
    }
    return parseInt(N * (N - 1) / 2) - ans;
}

// Driver Code

// Given array arr[]
let arr = [ 1, 2, 3, 4, 5, 6 ];

let N = arr.length;

// Function Call
document.write(findCount(arr, N));

// This code is contributed by subhammahato348

</script>
```

**Output**

```
11
```

***时间复杂度:** O(N)*

***空间复杂度:** O(32) = O(1)*