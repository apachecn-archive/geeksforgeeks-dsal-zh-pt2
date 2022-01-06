# 计算数组总和的因子对总和

> 原文:[https://www . geesforgeks . org/count-pair-sum-即数组的和因子/](https://www.geeksforgeeks.org/count-pair-sums-that-are-factors-of-the-sum-of-the-array/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】**，任务是找出对的数量，其中 **i ≤ j** ，这样对的和除以数组元素的[和。](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)

**示例:**

> **输入:** arr[] = {1，2，3，4，5}
> **输出:** 3
> **说明:**
> 下面是对数组之和进行除法的对(= 1 + 2 + 3 + 4 + 5 = 15):
> 
> 1.  (1，2):对的和= 1 + 2 = 3，除以和(= 15)。
> 2.  (1，4):对的和= 1 + 4 = 5，除以和(= 15)。
> 3.  (2，3):对的和= 2 + 3 = 5，除以和(= 15)。
> 
> 因此，对的计数是 3。
> 
> **输入:** arr[] = {1，5，2 }
> T3】输出: 0

**方法:**给定的问题可以通过[从给定的数组](https://www.geeksforgeeks.org/find-all-pairs-possible-from-the-given-array/)中生成所有可能的对 **(arr[i]，arr[j])** 来解决，使得 **i ≤ j** 并计算其元素之和除以数组之和[的所有对。检查所有可能的配对后，打印获得的总计数。](https://www.geeksforgeeks.org/program-find-sum-elements-given-array/)

下面是上述方法的实现。

## C++

```
// C++ program for the above approach

#include <iostream>
using namespace std;

// Function to find the number of pairs
// whose sums divides the sum of array
void countPairs(int arr[], int N)
{
    // Initialize the totalSum and
    // count as 0
    int count = 0, totalSum = 0;

    // Calculate the total sum of array
    for (int i = 0; i < N; i++) {
        totalSum += arr[i];
    }

    // Generate all possible pairs
    for (int i = 0; i < N; i++) {

        for (int j = i + 1; j < N; j++) {

            // If the sum is a factor
            // of totalSum or not
            if (totalSum
                    % (arr[i] + arr[j])
                == 0) {

                // Increment count by 1
                count += 1;
            }
        }
    }

    // Print the total count obtained
    cout << count;
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 3, 4, 5 };
    int N = sizeof(arr) / sizeof(arr[0]);
    countPairs(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG
{

    // Function to find the number of pairs
    // whose sums divides the sum of array
    public static void countPairs(int arr[], int N)
    {

        // Initialize the totalSum and
        // count as 0
        int count = 0, totalSum = 0;

        // Calculate the total sum of array
        for (int i = 0; i < N; i++)
        {
            totalSum += arr[i];
        }

        // Generate all possible pairs
        for (int i = 0; i < N; i++) {

            for (int j = i + 1; j < N; j++) {

                // If the sum is a factor
                // of totalSum or not
                if (totalSum % (arr[i] + arr[j]) == 0) {

                    // Increment count by 1
                    count += 1;
                }
            }
        }

        // Print the total count obtained
        System.out.println(count);
    }

  // Driver code
    public static void main(String[] args)
    {
        int arr[] = { 1, 2, 3, 4, 5 };
        int N = arr.length;
        countPairs(arr, N);

    }
}

 // This code is contributed by Potta Lokesh
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find the number of pairs
# whose sums divides the sum of array
def countPairs(arr, N):

    # Initialize the totalSum and
    # count as 0
    count = 0
    totalSum = 0

    # Calculate the total sum of array
    for i in range(N):
        totalSum += arr[i]

    # Generate all possible pairs
    for i in range(N):
        for j in range(i + 1, N, 1):

            # If the sum is a factor
            # of totalSum or not
            if (totalSum % (arr[i] + arr[j]) == 0):

                # Increment count by 1
                count += 1

    # Print the total count obtained
    print(count)

# Driver Code
if __name__ == '__main__':

    arr = [ 1, 2, 3, 4, 5 ]
    N = len(arr)

    countPairs(arr, N)

# This code is contributed by SURENDRA_GANGWAR
```

## C#

```
// C# program for the above approach
using System;

class GFG{

    // Function to find the number of pairs
    // whose sums divides the sum of array
    public static void countPairs(int[] arr, int N)
    {

        // Initialize the totalSum and
        // count as 0
        int count = 0, totalSum = 0;

        // Calculate the total sum of array
        for (int i = 0; i < N; i++)
        {
            totalSum += arr[i];
        }

        // Generate all possible pairs
        for (int i = 0; i < N; i++) {

            for (int j = i + 1; j < N; j++) {

                // If the sum is a factor
                // of totalSum or not
                if (totalSum % (arr[i] + arr[j]) == 0) {

                    // Increment count by 1
                    count += 1;
                }
            }
        }

        // Print the total count obtained
        Console.WriteLine(count);
    }

// Driver code
static public void Main()
{
    int[] arr = { 1, 2, 3, 4, 5 };
        int N = arr.Length;
        countPairs(arr, N);
}
}

// This code is contributed by splevel62.
```

## java 描述语言

```
<script>
        // JavaScript program for the above approach

        // Function to find the number of pairs
        // whose sums divides the sum of array
        function countPairs(arr, N)
        {

            // Initialize the totalSum and
            // count as 0
            let count = 0, totalSum = 0;

            // Calculate the total sum of array
            for (let i = 0; i < N; i++) {
                totalSum += arr[i];
            }

            // Generate all possible pairs
            for (let i = 0; i < N; i++)
            {
                for (let j = i + 1; j < N; j++)
                {

                    // If the sum is a factor
                    // of totalSum or not
                    if (totalSum
                        % (arr[i] + arr[j])
                        == 0) {

                        // Increment count by 1
                        count += 1;
                    }
                }
            }

            // Print the total count obtained
            document.write(count);
        }

        // Driver Code
        let arr = [1, 2, 3, 4, 5];
        let N = arr.length;
        countPairs(arr, N);

// This code is contributed by Potta Lokesh
    </script>
```

**Output:** 

```
3
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*