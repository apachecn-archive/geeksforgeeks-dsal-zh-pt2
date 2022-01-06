# 以 X 为最频繁元素的子阵计数，X 的每个值从 1 到 N

> 原文:[https://www . geeksforgeeks . org/以-x 作为从-1 到-n 的每个 x 值的最频繁元素的子数组计数/](https://www.geeksforgeeks.org/count-of-subarrays-with-x-as-the-most-frequent-element-for-each-value-of-x-from-1-to-n/)

给定一个大小为 **N、(**其中**0<A<= N**的[**arr【】】**，对于所有 **0 < =i < N** ，任务是为从 **1** 到 **N** 的每个编号 **X** 计算子阵列的数量，其中 **X** 在子阵中，多个元素具有最大频率，最小的元素应该被认为是最频繁的。](https://www.geeksforgeeks.org/array-data-structure/)

**示例:**

> **输入:** arr[]={2，1，2，3}，N=4
> **输出:**
> 4 5 1 0
> **解释:**
> 
> 1.  对于 X=1，X 是最常见元素的子阵列是{2，1}、{1}、{1，2}、{1，2，3}
> 2.  对于 X=2，X 是最常见元素的子阵列是{2}、{2，1，2}、{2，1，2，3}、{2}、{2，3}
> 3.  对于 X=3，X 是最常见元素的子阵列是{3}
> 4.  对于 X=4，没有包含 4 的子阵列。
> 
> **输入:** arr[]={3，1，5，1，3}，N=5
> **输出:**
> 12 0 2 0 1

**方法:**方法是使用两个循环跟踪每个[子阵列](https://www.geeksforgeeks.org/subarraysubstring-vs-subsequence-and-programs-to-generate-them/)中最频繁的元素，并将它们存储在单独的数组中。按照以下步骤解决问题:

1.  初始化一个大小为 **N** 到 **0** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **和**，以存储最终答案。
2.  从 **0** 迭代到 **N-1** ，对于每个当前索引 **i** ，执行以下操作:
    1.  初始化一个大小为 **N** 到 **0** 的[频率数组](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/) **计数**，存储从 **1** 到 **N** 各元素的当前频率。
    2.  将变量**最佳**初始化为 **0** ，以存储当前子阵列中最频繁的元素。
    3.  从 **i** 迭代到 **N-1** ，对于每个当前索引 **j** ，执行以下操作:
        1.  增加当前元素的**计数**，即**计数【arr[j]-1】=计数【arr[j]-1】+1**
        2.  检查当前元素的频率，即**arr【j】**是否大于 **best 的频率。**
        3.  检查电流元件**arr【j】**的频率是否等于 **best** 的频率，电流元件是否小于 **best** 。
        4.  如果其中任何一个为真，最好更新到当前元素，即**最好=arr[j]**
        5.  增加 **ans** 数组的**最佳**索引，即 **ans【最佳-1】= ans【最佳-1】+1**。
3.  打印数组**和**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate the number of subarrays where
// X(1<=X<=N) is the most frequent element
int mostFrequent(int arr[], int N)
{
    // array to store the final answers
    int ans[N] = { 0 };

    for (int i = 0; i < N; i++) {

        // Array to store current frequencies
        int count[N];

        // Initialise count
        memset(count, 0, sizeof(count));

        // Variable to store the
        // current most frequent element
        int best = 0;
        for (int j = i; j < N; j++) {

            // Update frequency array
            count[arr[j] - 1]++;
            if (count[arr[j] - 1] > count[best - 1]
                || (count[arr[j] - 1] == count[best - 1]
                    && arr[j] < best)) {
                best = arr[j];
            }

            // Update answer
            ans[best - 1]++;
        }
    }

    // Print answer
    for (int i = 0; i < N; i++)
        cout << ans[i] << " ";
}
// Driver code
int main()
{
    // Input
    int arr[] = { 2, 1, 2, 3 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // Function call
    mostFrequent(arr, N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG {

    // Function to calculate the number of subarrays where
    // X(1<=X<=N) is the most frequent element
    public static void mostFrequent(int[] arr, int N)
    {
        // array to store the final answers
        int[] ans = new int[N];

        for (int i = 0; i < N; i++) {

            // Array to store current frequencies
            int[] count = new int[N];

            // Variable to store the
            // current most frequent element
            int best = 1;
            for (int j = i; j < N; j++) {

                // Update frequency array
                count[arr[j] - 1]++;
                if (best > 0) {
                    if ((count[arr[j] - 1]
                         > count[best - 1])
                        || (count[arr[j] - 1]
                                == count[best - 1]
                            && arr[j] < best)) {
                        best = arr[j];
                    }

                    // Update answer
                    ans[best - 1]++;
                }
            }
        }

        // Print answer
        for (int i = 0; i < N; i++)
        System.out.print(ans[i] + " ");
    }

    // Driver Code
    public static void main(String[] args)
    {

     // Input
        int[] arr = { 2, 1, 2, 3 };
        int N = arr.length;

        // Function call
        mostFrequent(arr, N);
    }
}

// This code is contributed by sanjoy_62.
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to calculate the number of subarrays where
# X(1<=X<=N) is the most frequent element
def mostFrequent(arr, N):
    # array to store the final answers
    ans = [0]*N

    for i in range(N):
        # Array to store current frequencies
        count = [0]*N

        # Initialise count
        # memset(count, 0, sizeof(count))

        # Variable to store the
        # current most frequent element
        best = 0
        for j in range(i,N):
            # Update frequency array
            count[arr[j] - 1]+=1
            if (count[arr[j] - 1] > count[best - 1]
                or (count[arr[j] - 1] == count[best - 1]
                    and arr[j] < best)):
                best = arr[j]

            # Update answer
            ans[best - 1] += 1

    # Pranswer
    print(*ans)

# Driver code
if __name__ == '__main__':
    # Input
    arr= [2, 1, 2, 3]
    N = len(arr)

    # Function call
    mostFrequent(arr, N)

# This code is contributed by mohit kumar 29.
```

## C#

```
// C# program for the above approach
using System;
class GFG {

    // Function to calculate the number of subarrays where
    // X(1<=X<=N) is the most frequent element
    public static void mostFrequent(int[] arr, int N)
    {
        // array to store the final answers
        int[] ans = new int[N];

        for (int i = 0; i < N; i++) {

            // Array to store current frequencies
            int[] count = new int[N];

            // Variable to store the
            // current most frequent element
            int best = 1;
            for (int j = i; j < N; j++) {

                // Update frequency array
                count[arr[j] - 1]++;
                if (best > 0) {
                    if ((count[arr[j] - 1]
                         > count[best - 1])
                        || (count[arr[j] - 1]
                                == count[best - 1]
                            && arr[j] < best)) {
                        best = arr[j];
                    }

                    // Update answer
                    ans[best - 1]++;
                }
            }
        }

        // Print answer
        for (int i = 0; i < N; i++)
            Console.Write(ans[i] + " ");
    }

    // Driver code
    public static void Main()
    {

        // Input
        int[] arr = { 2, 1, 2, 3 };
        int N = arr.Length;

        // Function call
        mostFrequent(arr, N);
    }
}

// This code is contributed by subham348.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to calculate the number of subarrays where
// X(1<=X<=N) is the most frequent element
function mostFrequent(arr, N) {
    // array to store the final answers
    let ans = new Array(N).fill(0)

    for (let i = 0; i < N; i++) {

        // Array to store current frequencies
        let count = new Array(N);

        // Initialise count
        count.fill(0)

        // Variable to store the
        // current most frequent element
        let best = 1;
        for (let j = i; j < N; j++) {

            // Update frequency array
            count[arr[j] - 1]++;
            if (count[arr[j] - 1] > count[best - 1]
                || (count[arr[j] - 1] == count[best - 1]
                    && arr[j] < best)) {
                best = arr[j];
            }

            // Update answer
            ans[best - 1]++;
        }
    }

    // Print answer
    console.log(ans)
    for (let i = 0; i < N; i++)
        document.write(ans[i] + " ");
}

// Driver code
// Input
let arr = [2, 1, 2, 3];
let N = arr.length

// Function call
mostFrequent(arr, N);
</script>
```

**Output:** 

```
4 5 1 0
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*