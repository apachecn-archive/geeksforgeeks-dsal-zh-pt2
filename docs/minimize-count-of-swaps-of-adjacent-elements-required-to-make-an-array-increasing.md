# 最小化增加数组所需的相邻元素的交换次数

> 原文:[https://www . geeksforgeeks . org/最小化相邻元素的交换次数-需要增加数组数量/](https://www.geeksforgeeks.org/minimize-count-of-swaps-of-adjacent-elements-required-to-make-an-array-increasing/)

给定一个由第一个 **N 个**自然数的[排列组成的数组 **A[]** ，如果一个数组元素 **A[i]** 最多可以与其下一个相邻元素 **A[i+1]** 交换两次，那么任务就是找到将 **A[]** 修改为递增数组所需的最小操作数。如果无法将数组修改为递增数组，打印 **-1** 。](https://www.geeksforgeeks.org/find-permutation-of-first-n-natural-numbers-that-satisfies-the-given-condition/)

**示例:**

> **输入:**A[]=【2，1，5，3，4】
> **输出:** 3
> **说明:**
> 操作 1:交换(Arr[2]，Arr[3])。因此，A[]修改为{2，1，3，5，4}。
> 操作 2:交换(arr[3]，arr[4])。因此，A[]修改为{2，1，3，4，5}。
> 操作 3:交换(arr[0]，arr[1])。因此，A[]修改为{1，2，3，4，5}。
> 因此，操作顺序为:{2，1，5，3，4} → {2，1，3，5，4} → {2，1，3，4，5} → {1，2，3，4，5}
> 
> **输入:**A[]=【2，5，1，3，4】
> **输出:** -1

**方法:**这个想法是基于这样的观察:如果一个元素**A【I】**出现在索引 **i** 上，那么它一定是从索引**I–1**或**I–2**移动过来的。这是因为，从**I–2**左侧的指数转移到**A【I】**，互换的数量将超过 **2** 。因此，[反向遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)，检查**A【I】**是否在正确的位置。如果发现不是，检查**A【I–1】**和**A【I–2】**并相应更新操作计数。按照以下步骤解决问题:

*   [<u>使用变量遍历数组</u>](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) 、 **A[]** 越过索引**【N–1，0】**，比如 **i.**
    *   将正确的索引值存储在一个变量中，比如说 **X** 为 **i + 1** 。
    *   如果 **A[i]** 当前不在其正确位置，即 **A[i]** 不等于 **X** ，则执行以下步骤:
        *   如果**A【I–1】**的值等于 **X** ，则以 **1** 和 [<u>递增**计数**，并交换</u>](https://www.geeksforgeeks.org/swap-two-numbers-without-using-temporary-variable/)**A【I】**和**A【I-1】**。
        *   否则，如果**A【I–2】**的值等于 **X** ，则以 **2** 和 [<u>递增**计数**交换</u>](https://www.geeksforgeeks.org/swap-two-numbers-without-using-temporary-variable/) 对**A【I–2】**和**A【I–1】**，则**A【I–2】**和**A【I】**。
        *   否则，将**计数**的值更新为 **-1** 和 [<u>脱离循环</u>](https://www.geeksforgeeks.org/break-statement-cc/) ，因为**A【I】**不能交换超过**两次**。
*   完成数组遍历后，打印**计数**的值作为结果。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count minimum number of
// operations required to obtain an
// increasing array from given array A[]
void minimumOperations(int A[], int n)
{
    // Store the required result
    int cnt = 0;

    // Traverse the array A[]
    for (int i = n - 1; i >= 0; i--) {

        // If the current element is not
        // in its correct position
        if (A[i] != (i + 1)) {

            // Check if it is present at index i - 1
            if (((i - 1) >= 0)
                && A[i - 1] == (i + 1)) {
                cnt++;
                swap(A[i], A[i - 1]);
            }

            // Check if it is present at index i-2
            else if (((i - 2) >= 0)
                     && A[i - 2] == (i + 1)) {
                cnt += 2;
                A[i - 2] = A[i - 1];
                A[i - 1] = A[i];
                A[i] = i + 1;
            }

            // Otherwise, print -1 (Since A[i]
            // can not be swapped more than twice)
            else {
                cout << -1;
                return;
            }
        }
    }

    // Print the result
    cout << cnt;
}

// Driver Code
int main()
{
    // Given array
    int A[] = {7, 3, 2, 1, 4 };

    // Store the size of the array
    int n = sizeof(A) / sizeof(A[0]);

    minimumOperations(A, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
import java.lang.*;

class GFG{

// Function to count minimum number of
// operations required to obtain an
// increasing array from given array A[]
static void minimumOperations(int A[], int n)
{

    // Store the required result
    int cnt = 0;

    // Traverse the array A[]
    for(int i = n - 1; i >= 0; i--)
    {

        // If the current element is not
        // in its correct position
        if (A[i] != (i + 1))
        {

            // Check if it is present at index i - 1
            if (((i - 1) >= 0) &&
                A[i - 1] == (i + 1))
            {
                cnt++;
                int t = A[i];
                A[i] = A[i-1];
                A[i-1] = t;
            }

            // Check if it is present at index i-2
            else if (((i - 2) >= 0) &&
                     A[i - 2] == (i + 1))
            {
                cnt += 2;
                A[i - 2] = A[i - 1];
                A[i - 1] = A[i];
                A[i] = i + 1;
            }

            // Otherwise, print -1 (Since A[i]
            // can not be swapped more than twice)
            else
            {
                System.out.println(-1);
                return;
            }
        }
    }

    // Print the result
    System.out.println(cnt);
}

// Driver code
public static void main(String[] args)
{

    // Given array
    int A[] = { 7, 3, 2, 1, 4 };

    // Store the size of the array
    int n = A.length;

    minimumOperations(A, n);
}
}

// This code is contributed by souravghosh0416
```

## 蟒蛇 3

```
# Python 3 program for the above approach

# Function to count minimum number of
# operations required to obtain an
# increasing array from given array A[]
def minimumOperations(A, n):

    # Store the required result
    cnt = 0

    # Traverse the array A[]
    for i in range(n - 1, -1, -1):

        # If the current element is not
        # in its correct position
        if (A[i] != (i + 1)):

            # Check if it is present at index i - 1
            if (((i - 1) >= 0)
                    and A[i - 1] == (i + 1)):
                cnt += 1
                A[i], A[i - 1] = A[i - 1], A[i]

            # Check if it is present at index i-2
            elif (((i - 2) >= 0)
                  and A[i - 2] == (i + 1)):
                cnt += 2
                A[i - 2] = A[i - 1]
                A[i - 1] = A[i]
                A[i] = i + 1

            # Otherwise, print -1 (Since A[i]
            # can not be swapped more than twice)
            else:
                print(-1)
                return

    # Print the result
    print(cnt)

# Driver Code
if __name__ == "__main__":

    # Given array
    A = [7, 3, 2, 1, 4]

    # Store the size of the array
    n = len(A)

    minimumOperations(A, n)

    # Thi code is contributed by ukasp.
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to count minimum number of
// operations required to obtain an
// increasing array from given array A[]
static void minimumOperations(int []A, int n)
{

    // Store the required result
    int cnt = 0;

    // Traverse the array A[]
    for(int i = n - 1; i >= 0; i--)
    {

        // If the current element is not
        // in its correct position
        if (A[i] != (i + 1))
        {

            // Check if it is present at index i - 1
            if (((i - 1) >= 0) &&
                A[i - 1] == (i + 1))
            {
                cnt++;
                int t = A[i];
                A[i] = A[i-1];
                A[i-1] = t;
            }

            // Check if it is present at index i-2
            else if (((i - 2) >= 0) &&
                     A[i - 2] == (i + 1))
            {
                cnt += 2;
                A[i - 2] = A[i - 1];
                A[i - 1] = A[i];
                A[i] = i + 1;
            }

            // Otherwise, print -1 (Since A[i]
            // can not be swapped more than twice)
            else
            {
                Console.WriteLine(-1);
                return;
            }
        }
    }

    // Print the result
    Console.WriteLine(cnt);
}

// Driver code
public static void Main()
{

    // Given array
    int []A = { 7, 3, 2, 1, 4 };

    // Store the size of the array
    int n = A.Length;

    minimumOperations(A, n);
}
}

// This code is contributed by importantly.
```

## java 描述语言

```
<script>

// Javascript program for the above approach   

// Function to count minimum number of
    // operations required to obtain an
    // increasing array from given array A
    function minimumOperations(A , n) {

        // Store the required result
        var cnt = 0;

        // Traverse the array A
        for (i = n - 1; i >= 0; i--) {

            // If the current element is not
            // in its correct position
            if (A[i] != (i + 1)) {

                // Check if it is present at index i - 1
                if (((i - 1) >= 0) && A[i - 1] == (i + 1)) {
                    cnt++;
                    var t = A[i];
                    A[i] = A[i - 1];
                    A[i - 1] = t;
                }

                // Check if it is present at index i-2
                else if (((i - 2) >= 0) && A[i - 2] == (i + 1)) {
                    cnt += 2;
                    A[i - 2] = A[i - 1];
                    A[i - 1] = A[i];
                    A[i] = i + 1;
                }

                // Otherwise, print -1 (Since A[i]
                // can not be swapped more than twice)
                else {
                    document.write(-1);
                    return;
                }
            }
        }

        // print the result
        document.write(cnt);
    }

    // Driver code

        // Given array
        var A = [ 7, 3, 2, 1, 4 ];

        // Store the size of the array
        var n = A.length;

        minimumOperations(A, n);

// This code contributed by Rajput-Ji

</script>
```

**Output:** 

```
-1
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)