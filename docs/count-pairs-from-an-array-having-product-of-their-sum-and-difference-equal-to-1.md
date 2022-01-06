# 从其和与差的乘积等于 1 的数组中计数对

> 原文:[https://www . geeksforgeeks . org/从一个数组中计数对，使它们的和与差的乘积等于 1/](https://www.geeksforgeeks.org/count-pairs-from-an-array-having-product-of-their-sum-and-difference-equal-to-1/)

给定大小为 **N** 的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，任务是计算可能的数组元素对 **(arr[i]，arr[j])** ，使得**(arr[I]+arr[j])*(arr[I]–arr[j])**为 1。

**示例:**

> **输入:** arr[] = {3，1，1，0}
> **输出:** 2
> **解释:**
> 这两个可能的对是:
> 
> 1.  (arr[1]+arr[3])*(arr[1]–arr[3])= 1
> 2.  (arr[2]+arr[3])*(arr[2]–arr[3])= 1
> 
> **输入:** arr[] = {12，0，1，1，14，0，9，0}
> **输出:** 4
> **解释:**
> 四种可能的配对如下:
> 
> 1.  (3，6):(arr[3]+arr[6])*(arr[3]–arr[6])= 1
> 2.  (4，6):(arr[4]+arr[6])*(arr[4]–arr[6])= 1
> 3.  (3，8):(arr[3]+arr[8])*(arr[3]–arr[8])= 1
> 4.  (3，6):(arr[4]+arr[8])*(arr[4]–arr[8])= 1

**天真方法:**最简单的方法是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)和[从给定的数组](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)中生成所有可能的对，并计算那些和与差的乘积为 1 的对。最后，打印完成上述步骤后获得的最终计数。

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*

**有效方法:**对于任意一对数组元素 **(arr[i]，arr[j])** 给定的条件可以表示为:

> (arr[I]+arr[j])*(arr[I]–arr[j])= 1
> =>(arr[I]<sup>2</sup>–arr[j]<sup>2</sup>)= 1

因此，可以得出结论，仅通过配对 **arr[i] = 1** 和 **arr[j] = 0** 和 **i < j** 就可以满足要求的条件。按照以下步骤解决问题:

*   初始化两个变量， **oneCount** 和 **desiredPairs** 分别存储 1 的计数和所需的对。
*   [遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并检查以下内容:
    *   **如果 arr[i] = 1:** 将**计数**增加 **1** 。
    *   **如果 arr[i] = 0:** 将目前获得的 **1** 的计数加到 **desiredPairs** 上。
*   完成上述步骤后，打印 **desiredPairs** 的值作为所需答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count the desired
// number of pairs
int countPairs(int arr[], int n)
{
    // Initialize oneCount
    int oneCount = 0;

    // Initialize the desiredPair
    int desiredPair = 0;

    // Traverse the given array
    for (int i = 0; i < n; i++) {

        // If 1 is encountered
        if (arr[i] == 1) {
            oneCount++;
        }

        // If 0 is encountered
        if (arr[i] == 0) {

            // Update count of pairs
            desiredPair += oneCount;
        }
    }

    // Return the final count
    return desiredPair;
}

// Driver Code
int main()
{
    // Given array arr[]
    int arr[] = { 3, 1, 1, 0 };
    int N = sizeof(arr) / sizeof(arr[0]);
    // Function Call
    cout << countPairs(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG{

// Function to count the desired
// number of pairs
static int countPairs(int arr[], int n)
{

    // Initialize oneCount
    int oneCount = 0;

    // Initialize the desiredPair
    int desiredPair = 0;

    // Traverse the given array
    for(int i = 0; i < n; i++)
    {

        // If 1 is encountered
        if (arr[i] == 1)
        {
            oneCount++;
        }

        // If 0 is encountered
        if (arr[i] == 0)
        {

            // Update count of pairs
            desiredPair += oneCount;
        }
    }

    // Return the final count
    return desiredPair;
}

// Driver Code
public static void main(String[] args)
{

    // Given array arr[]
    int arr[] = { 3, 1, 1, 0 };
    int N = arr.length;

    // Function call
    System.out.println(countPairs(arr, N));
}
}

// This code is contributed by sanjoy_62
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to count the desired
# number of pairs
def countPairs(arr, n):

    # Initialize oneCount
    oneCount = 0

    # Initialize the desiredPair
    desiredPair = 0

    # Traverse the given array
    for i in range(n):

        # If 1 is encountered
        if (arr[i] == 1):
            oneCount += 1

        # If 0 is encountered
        if (arr[i] == 0):

            # Update count of pairs
            desiredPair += oneCount

    # Return the final count
    return desiredPair

# Driver Code
if __name__ == '__main__':

    # Given array arr[]
    arr = [ 3, 1, 1, 0 ]
    N = len(arr)

    # Function call
    print(countPairs(arr, N))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to count the desired
// number of pairs
static int countPairs(int []arr, int n)
{

    // Initialize oneCount
    int oneCount = 0;

    // Initialize the desiredPair
    int desiredPair = 0;

    // Traverse the given array
    for(int i = 0; i < n; i++)
    {

        // If 1 is encountered
        if (arr[i] == 1)
        {
            oneCount++;
        }

        // If 0 is encountered
        if (arr[i] == 0)
        {

            // Update count of pairs
            desiredPair += oneCount;
        }
    }

    // Return the readonly count
    return desiredPair;
}

// Driver Code
public static void Main(String[] args)
{

    // Given array []arr
    int []arr = { 3, 1, 1, 0 };
    int N = arr.Length;

    // Function call
    Console.WriteLine(countPairs(arr, N));
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to count the desired
// number of pairs
function countPairs(arr, n)
{

    // Initialize oneCount
    let oneCount = 0;

    // Initialize the desiredPair
    let desiredPair = 0;

    // Traverse the given array
    for(let i = 0; i < n; i++)
    {

        // If 1 is encountered
        if (arr[i] == 1)
        {
            oneCount++;
        }

        // If 0 is encountered
        if (arr[i] == 0)
        {

            // Update count of pairs
            desiredPair += oneCount;
        }
    }

    // Return the final count
    return desiredPair;
}

// Driver Code

// Given array arr[]
let arr = [ 3, 1, 1, 0 ];
let N = arr.length;

// Function call
document.write(countPairs(arr, N));

// This code is contributed by target_2

</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)