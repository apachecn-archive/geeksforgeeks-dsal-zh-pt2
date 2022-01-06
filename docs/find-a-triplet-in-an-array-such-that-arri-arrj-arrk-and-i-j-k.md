# 在数组中找到一个三元组，使得 arr[i] arr[k]和 i < j < k

> 原文:[https://www . geesforgeks . org/find-a-三元组-in-a-arri-arrj-arrk-and-I-j-k/](https://www.geeksforgeeks.org/find-a-triplet-in-an-array-such-that-arri-arrj-arrk-and-i-j-k/)

给定一个由第一个 **N** 个自然数的排列组成的[数组](https://www.geeksforgeeks.org/array-data-structure/)**arr【】**，任务是从给定数组中找到一个三元组 **(i，j，k)** ，使得**arr【I】<arr【j】>arr【k】**，其中 **(i < j < k)** 。如果存在多个三元组，则打印任何有效的三元组索引。否则，打印 **-1** 。

**示例:**

> **输入:** arr[] = {2，1，4，3}
> **输出:** 1 2 3
> **说明:**满足给定条件的三元组为(arr[1]，arr[2]，arr[3])
> 因此，需要的输出为 **1 2 3** 。
> 
> **输入:** arr[] = {1，2，3，4，5}
> **输出:** -1

**天真方法:**解决这个问题最简单的方法是[遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)和[生成给定数组的所有可能三元组](https://www.geeksforgeeks.org/print-all-triplets-with-given-sum/)，对于每个三元组，检查其是否满足给定条件。如果发现是真的，那就打印出来。否则，打印 **-1** 。

***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(1)*

**高效方法:**为了优化上述方法，该想法基于以下观察:

*   [如果给定数组从索引范围**【1，N–2】**开始按升序或降序排序](https://www.geeksforgeeks.org/program-check-array-sorted-not-iterative-recursive/)，则该解不存在。
*   否则，在给定的数组中至少存在一个索引，使得紧接在该索引之前和之后的元素小于当前元素。

按照以下步骤解决问题:

*   [遍历给定数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，对于每个数组索引，检查当前索引前后的元素是否小于当前元素。如果发现是真的，那就打印那个三联体**(I–1，I，i + 1)** 。
*   否则，打印 **-1** 。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach
#include <iostream>
using namespace std;

// Function to find a triplet
// that satisfy the conditions
void FindTrip(int arr[], int N)
{

    // Traverse the given array
    for(int i = 1; i < N - 1; i++)
    {

        // Stores current element
        int p = arr[i - 1];

        // Stores element just before
        // the current element
        int q = arr[i];

        // Stores element just after
        // the current element
        int r = arr[i + 1];

        // Check the given conditions
        if (p < q && q > r)
        {

            // Print a triplet
            cout << i - 1 << " "
                 << i << " " << i + 1;

            return;
        }
    }

    // If no triplet found
    cout << -1;
}

// Driver Code
int main()
{
    int arr[] = { 2, 1, 4, 3 };

    int N = sizeof(arr) / sizeof(arr[0]);

    FindTrip(arr, N);

    return 0;
}

// This code is contributed by jyoti369
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
class GFG {

    // Function to find a triplet
    // that satisfy the conditions
    static void FindTrip(int arr[],
                        int N)
    {
        // Traverse the given array
        for (int i = 1; i < N - 1;
            i++) {

            // Stores current element
            int p = arr[i - 1];

            // Stores element just before
            // the current element
            int q = arr[i];

            // Stores element just after
            // the current element
            int r = arr[i + 1];

            // Check the given conditions
            if (p < q && q > r) {

                // Print a triplet
                System.out.println(
                    (i - 1) + " "
                    + (i) + " "
                    + (i + 1));
                return;
            }
        }

        // If no triplet found
        System.out.println(-1);
    }

    // Driver Code
    public static void main(String args[])
    {
        int arr[] = { 2, 1, 4, 3 };

        int N = arr.length;
        FindTrip(arr, N);
    }
}
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to find a triplet
# that satisfy the conditions
def FindTrip(arr, N):

    # Traverse the given array
    for i in range(1, N - 1):

        # Stores current element
        p = arr[i - 1]

        # Stores element just before
        # the current element
        q = arr[i]

        # Stores element just after
        # the current element
        r = arr[i + 1]

        # Check the given conditions
        if (p < q and q > r):

            # Print a triplet
            print(i - 1, i, i + 1)

            return

    # If no triplet found
    print(-1)

# Driver Code
if __name__ == '__main__':

    arr = [ 2, 1, 4, 3 ]

    N = len(arr)

    FindTrip(arr, N)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to implement
// the above approach 
using System;

class GFG{

// Function to find a triplet
// that satisfy the conditions
static void FindTrip(int[] arr, int N)
{

    // Traverse the given array
    for(int i = 1; i < N - 1; i++)
    {

        // Stores current element
        int p = arr[i - 1];

        // Stores element just before
        // the current element
        int q = arr[i];

        // Stores element just after
        // the current element
        int r = arr[i + 1];

        // Check the given conditions
        if (p < q && q > r)
        {

            // Print a triplet
            Console.WriteLine((i - 1) + " " +
                              (i) + " " + (i + 1));
            return;
        }
    }

    // If no triplet found
    Console.WriteLine(-1);
}

// Driver Code
public static void Main()
{
    int[] arr = { 2, 1, 4, 3 };
    int N = arr.Length;

    FindTrip(arr, N);
}
}

// This code is contributed by code_hunt
```

## java 描述语言

```
<script>
// Javascript program to implement
// the above approach

    // Function to find a triplet
    // that satisfy the conditions
    function FindTrip(arr, N)
    {
        // Traverse the given array
        for (let i = 1; i < N - 1;
            i++) {

            // Stores current element
            let p = arr[i - 1];

            // Stores element just before
            // the current element
            let q = arr[i];

            // Stores element just after
            // the current element
            let r = arr[i + 1];

            // Check the given conditions
            if (p < q && q > r) {

                // Prlet a triplet
                document.write(
                    (i - 1) + " "
                    + (i) + " "
                    + (i + 1));
                return;
            }
        }

        // If no triplet found
        document.write(-1);
    }

    // Driver Code

           let arr = [2, 1, 4, 3 ];

        let N = arr.length;
        FindTrip(arr, N);

</script>
```

**输出:**

```
1 2 3
```

***时间复杂度:** O(N)*

***辅助空间:**O(1)*T4】