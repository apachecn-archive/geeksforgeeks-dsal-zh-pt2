# 对给定数组中按位“与”超过按位“异或”的对进行计数

> 原文:[https://www . geeksforgeeks . org/count-pairs-with-bitwise-and-over-bitwise-xor-from-a-给定数组/](https://www.geeksforgeeks.org/count-pairs-whose-bitwise-and-exceeds-bitwise-xor-from-a-given-array/)

给定一个大小为 **N** 的 [<u>数组</u>](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是计算给定数组中的对的数量，使得每对的 [<u>位 AND ( & )</u>](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/) 大于其 [<u>位 XOR(^)</u>](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/) 。

**示例:**

> **输入:** *arr[] = {1，2，3，4}*
> **输出:** 1
> **解释:**
> *满足给定条件的对为:*
> (2&3)>(2 ^ 3)
> *因此，所需输出为 1。*
> 
> ***输入:** arr[] = {* 1，4，3，7}
> **输出:** 1
> **解释:**
> *满足给定条件的对为:*
> **(4&7)>(4 ^ 3)
> *因此，所需输出为 1。***

****天真方法:**解决问题最简单的方法是 [<u>遍历数组</u>](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) 和 [<u>从给定数组</u>](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/) 生成所有可能的对。对于每一对，检查其**位与** ( ***&*** )是否大于其**位异或** ( **^** )。如果发现为真，则通过 **1** 增加对的计数。最后，打印获得的这种对的计数。**

*****时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)***

****高效方法:**要优化上述方法，请遵循 [<u>逐位运算符</u>](https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/) 的属性:**

> ***1 ^ 0 = 1*
> *0 ^ 1 = 1*
> *1&1 = 1*
> T9】x = b<sub>31</sub>b<sub>30</sub>…..b<sub>1</sub>b<sub>0</sub>
> *Y = a<sub>31</sub>b<sub>30</sub>…。a<sub>1</sub>a<sub>0</sub>*
> *如果表达式 **{(X & Y) > (X ^ Y)}** 为真，则 **X** 和 **Y** 的**最高有效位(MSB)** 必须相等。*
> *满足条件 **{(X & Y) > (X ^ Y)}** 的配对总数等于:*
> ![\Sigma_{n=0}^{31}(^{bit[i]}_{\ \ \ 2})](img/65f7172548c99bb1664646bda5fbd334.png "Rendered by QuickLaTeX.com")**

**按照以下步骤解决问题:**

1.  **初始化一个变量，比如 **res** ，以存储满足给定条件的对的计数。**
2.  **[遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr[]** 。**
3.  **存储给定数组的每个元素的**最高有效位(*****【MSB】*****)**的位置。**
4.  **初始化大小为 **32** 的数组**位[]、**(最大位数)**
5.  **[迭代每个数组元素](https://www.geeksforgeeks.org/iterating-arrays-java/)并执行以下步骤:

    1.  找到当前数组元素的**最高有效位(******)**，说 **j** 。**
    2.  **将存储在**位【j】**中的值添加到答案中。**
    3.  **将**位【j】**的值增加 **1** 。**** 

****下面是上述方法的实现****

## ****C++****

```
**// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count pairs that
// satisfy the above condition
int cntPairs(int arr[], int N)
{

    // Stores the count of pairs
    int res = 0;

    // Stores the count of array
    // elements having same
    // positions of MSB
    int bit[32] = { 0 };

    // Traverse the array
    for (int i = 0; i < N; i++) {
        // Stores the index of
        // MSB of array elements
        int pos = log2(arr[i]);
        bit[pos]++;
    }

    // Calculate number of pairs
    for (int i = 0; i < 32; i++) {
        res += (bit[i] * (bit[i] - 1)) / 2;
    }

    return res;
}

// Driver Code
int main()
{
    // Given Input
    int arr[] = { 1, 2, 3, 4 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function call to count pairs
    // satisfying the given condition
    cout << cntPairs(arr, N);
}**
```

## ****Java 语言(一种计算机语言，尤用于创建网站)****

```
**// Java program to implement
// the above approach
import java.io.*;

class GFG{

// Function to count pairs that
// satisfy the above condition
static int cntPairs(int arr[], int N)
{

    // Stores the count of pairs
    int res = 0;

    // Stores the count of array
    // elements having same
    // positions of MSB
    int bit[] = new int[32];

    // Traverse the array
    for(int i = 0; i < N; i++)
    {

        // Stores the index of
        // MSB of array elements
        int pos = (int)(Math.log(arr[i]) / Math.log(2));
        bit[pos]++;
    }

    // Calculate number of pairs
    for(int i = 0; i < 32; i++)
    {
        res += (bit[i] * (bit[i] - 1)) / 2;
    }
    return res;
}

// Driver Code
public static void main(String[] args)
{

    // Given Input
    int arr[] = { 1, 2, 3, 4 };
    int N = arr.length;

    // Function call to count pairs
    // satisfying the given condition
    System.out.println(cntPairs(arr, N));
}
}

// This code is contributed by Dharanendra L V.**
```

## ****蟒蛇 3****

```
**# Python3 program to implement
# the above approach
import math

# Function to count pairs that
# satisfy the above condition
def cntPairs(arr, N):

    # Stores the count of pairs
    res = 0

    # Stores the count of array
    # elements having same
    # positions of MSB
    bit = [0] * 32

    # Traverse the array
    for i in range(N):

        # Stores the index of
        # MSB of array elements
        pos = (int)(math.log2(arr[i]))
        bit[pos] += 1

    # Calculate number of pairs
    for i in range(32):
        res += (bit[i] * (bit[i] - 1)) // 2

    return res

# Driver Code
if __name__ == "__main__":

    # Given Input
    arr = [1, 2, 3, 4]
    N = len(arr)

    # Function call to count pairs
    # satisfying the given condition
    print(cntPairs(arr, N))

# This code is contributed by ukasp**
```

## ****C#****

```
**// C# program to implement
// the above approach
using System;

class GFG{

// Function to count pairs that
// satisfy the above condition
static int cntPairs(int[] arr, int N)
{

    // Stores the count of pairs
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
        int pos = (int)(Math.Log(arr[i]) / Math.Log(2));
        bit[pos]++;
    }

    // Calculate number of pairs
    for(int i = 0; i < 32; i++)
    {
        res += (bit[i] * (bit[i] - 1)) / 2;
    }
    return res;
}

// Driver Code
static public void Main ()
{

    // Given Input
    int[] arr = { 1, 2, 3, 4 };
    int N = arr.Length;

    // Function call to count pairs
    // satisfying the given condition
    Console.Write(cntPairs(arr, N));
}
}

// This code is contributed by avijitmondal1998**
```

## ****java 描述语言****

```
**<script>

// Javascript program to implement
// the above approach

// Function to count pairs that
// satisfy the above condition
function cntPairs(arr, N)
{

    // Stores the count of pairs
    var res = 0;

    // Stores the count of array
    // elements having same
    // positions of MSB
    var bit  = Array(32).fill(0);
    var i;
    // Traverse the array
    for( i = 0; i < N; i++) {
        // Stores the index of
        // MSB of array elements
        var pos = Math.ceil(Math.log2(arr[i]));
        bit[pos] += 1;
    }

    // Calculate number of pairs
    for (i = 0; i < 32; i++) {
        res += Math.ceil((bit[i] * (bit[i] - 1)) / 2);
    }

    return res;
}

// Driver Code
    // Given Input
    arr = [1, 2, 3, 4];
    N = arr.length;

    // Function call to count pairs
    // satisfying the given condition
    document.write(cntPairs(arr, N));

</script>**
```

******Output:** 

```
1
```**** 

*******时间复杂度:**O(N)*
T5**辅助空间:** O(1)****