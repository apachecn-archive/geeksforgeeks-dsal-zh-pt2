# 自动缩放后在时间帧结束时查找实例

> 原文:[https://www . geeksforgeeks . org/find-自动缩放后时间帧结束时的实例/](https://www.geeksforgeeks.org/find-instances-at-end-of-time-frame-after-auto-scaling/)

给定一个整数、**实例**和一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/)、**arr【】**表示计算系统每秒的平均利用率百分比，任务是在时间帧结束时找到**实例**的数量，以便计算系统根据以下规则自动调整**实例**的数量:

> *   **平均利用率<25%**如果实例数量大于 1，则将实例数量减少一半。
> *   **25% ≤平均利用率≤60%**不采取行动。
> *   **平均利用率>60%**如果翻倍值不超过**2 * 10<sup>8</sup>T5】，则实例数翻倍。**
> 
> 一旦执行添加或减少实例数量的操作，系统将停止监控 10 秒钟。在此期间，实例的数量不会改变。

**示例:**

> **输入:**实例= 2，arr[] = {25，23，1，2，3，4，5，6，7，8，9，10，76，80}
> **输出:** 2
> **解释:**
> 在第二个 1，arr[0] = 25 ≤ 25，因此不采取任何行动。
> 在第二个 2，arr[1] = 23 < 25，因此一个动作被实例化以将实例数量减半至上限(2/2) = 1。系统将停止检查 10 秒钟，因此从 arr[2]到 arr[11]不会采取任何措施。
> 在第二个 13，arr[12] = 76 > 60，因此实例数量从 1 增加到 2。
> 
> 没有更多的读数需要考虑，2 是最终值。
> 
> **输入:**实例= 5，arr = {30，5，4，8，19，89}
> **输出:** 3
> **解释:**
> 在第二个 1，25 ≤ arr[0] = 30 ≤ 60，因此不采取任何行动。
> 在第二个 2，arr[1] = 5 < 25，因此一个动作被实例化以将实例数量减半至上限(5/2) = 3。
> 系统将停止检查 10 秒，因此从 arr[2]到 arr[5]不会采取任何行动。
> 
> 没有更多的阅读材料需要考虑，3 是最终答案。

**方法:**给定的问题可以通过[遍历给定的数组**arr【】**](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)来解决，如果当前元素小于 25，那么如果实例数大于 1，则将实例数除以 2。否则，如果当前值大于 60，则实例数乘以 2，如果实例数不大于 10 <sup>8</sup> ，则在执行两个操作中的任何一个后，将当前索引增加 10。按照以下步骤解决问题:

*   [使用变量 **i** 遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)、 **arr[]** ，并执行以下步骤:
    *   如果**arr【I】**小于 25 且**实例**大于 1，则将**实例**除以 2，并将 **i** 增加 **10** 。
    *   如果**arr【I】**大于 60 且**实例**小于或等于 10 <sup>8</sup> ，则将**实例**乘以 2，并将 **i** 增加 **10** 。
    *   将指数 **i** 增加 **1** 。
*   完成上述步骤后，打印**实例的数量**作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the number of
// instances after compintion
void finalInstances(int instances,
                                  int arr[], int N)
{
    int i = 0;

    // Traverse the array, arr[]
    while (i < N)
    {

        // If current element is less
        // than 25
        if (arr[i] < 25 && instances > 1)
        {

            // Divide instances by 2 and take ceil value
            double temp = (instances / 2.0);
            instances = (int)(ceil(temp));
            i = i + 10;
        }

        // If the current element is
        // greater than 60
        else if (arr[i] > 60 &&
                 instances <= (2*pow(10, 8)))
        {

            // Double the instances
            instances = instances * 2;
            i = i + 10;
        }
        i = i + 1;
    }

    // Print the instances at the end
    // of the traversal
    cout << instances;
}

// Driver Code
int main()
{
    int instances = 2;
    int arr[] = { 25, 23, 1, 2, 3, 4, 5,
                  6, 7, 8, 9, 10, 76, 80 };

    int N = sizeof(arr) / sizeof(arr[0]);

    // Function Call
    finalInstances(instances, arr, N);
}

// This code is contributed by splevel62
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for above approach
class GFG{

// Function to find the number of
// instances after compintion
public static void finalInstances(int instances,
                                  int[] arr)
{
    int i = 0;

    // Traverse the array, arr[]
    while (i < arr.length)
    {

        // If current element is less
        // than 25
        if (arr[i] < 25 && instances > 1)
        {

            // Divide instances by 2
            instances = (instances / 2);
            i = i + 10;
        }

        // If the current element is
        // greater than 60
        else if (arr[i] > 60 &&
                 instances <= Math.pow(10, 8))
        {

            // Double the instances
            instances = instances * 2;
            i = i + 10;
        }
        i = i + 1;
    }

    // Print the instances at the end
    // of the traversal
    System.out.println(instances);
}

// Driver Code
public static void main(String args[])
{
    int instances = 2;
    int[] arr = { 25, 23, 1, 2, 3, 4, 5,
                  6, 7, 8, 9, 10, 76, 80 };

    // Function Call
    finalInstances(instances, arr);
}
}

// This code is contributed by _saurabh_jaiswal
```

## 蟒蛇 3

```
# Python program for the above approach
from math import ceil

# Function to find the number of
# instances after completion
def finalInstances(instances, arr):
    i = 0

    # Traverse the array, arr[]
    while i < len(arr):

        # If current element is less
        # than 25
        if arr[i] < 25 and instances > 1:

            # Divide instances by 2
            instances = ceil(instances / 2)
            i += 10

        # If the current element is
        # greater than 60
        elif arr[i] > 60 and instances <= 10**8:

            # Double the instances
            instances *= 2
            i += 10
        i += 1

    # Print the instances at the end
    # of the traversal
    print(instances)

# Driver Code
instances = 2

arr = [25, 23, 1, 2, 3, 4, 5,
       6, 7, 8, 9, 10, 76, 80]

# Function Call
finalInstances(instances, arr)
```

## C#

```
// C# program for above approach
using System;

class GFG{

// Function to find the number of
// instances after compintion
static void finalInstances(int instances, int[] arr)
{
        int i = 0;

        // Traverse the array, arr[]
        while (i < arr.Length) {

            // If current element is less
            // than 25
            if (arr[i] < 25 && instances > 1) {

                // Divide instances by 2
                instances = (instances / 2);
                i = i + 10;
            }

            // If the current element is
            // greater than 60
            else if (arr[i] > 60 && instances <= Math.Pow(10, 8))
            {

                // Double the instances
                instances = instances * 2;
                i = i + 10;

            }
            i = i + 1;

        }
        // Print the instances at the end
        // of the traversal
        Console.Write(instances);
    }

// Driver Code
static void Main()
{
    int instances = 2;

    int[] arr = {25, 23, 1, 2, 3, 4, 5,
        6, 7, 8, 9, 10, 76, 80};

    // Function Call
    finalInstances(instances, arr);
}
}

// This code is contributed by sanjoy_62.
```

## java 描述语言

```
<script>

        // JavaScript Program for the above approach

        // Function to find the number of
        // instances after completion
        function finalInstances(instances, arr) {
            let i = 0;

            // Traverse the array, arr[]
            while (i < arr.length) {

                // If current element is less
                // than 25
                if (arr[i] < 25 && instances > 1) {

                    // Divide instances by 2
                    instances = Math.ceil(instances / 2);
                    i = i + 10;
                }

                // If the current element is
                // greater than 60
                else if (arr[i] > 60 && instances <= Math.pow(10, 8))
                {

                    // Double the instances
                    instances = instances * 2;
                    i = i + 10;

                }
                i = i + 1;

            }
            // Print the instances at the end
            // of the traversal
            document.write(instances);
        }
        // Driver Code
        let instances = 2;

        let arr = [25, 23, 1, 2, 3, 4, 5,
            6, 7, 8, 9, 10, 76, 80];

        // Function Call
        finalInstances(instances, arr);

    // This code is contributed by Potta Lokesh

</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)