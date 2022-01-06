# 通过循环移位一个段或者用最大值替换前缀来最小化步骤以使所有数组元素相等

> 原文:[https://www . geeksforgeeks . org/最小化使所有数组元素相等的步骤循环移位一个段或最大化替换前缀/](https://www.geeksforgeeks.org/minimize-steps-to-make-all-array-elements-equal-by-cyclically-shifting-a-segment-or-replacing-prefix-by-maximum/)

给定一个由 **N** 正整数组成的数组 **arr[]** ，任务是通过对该数组执行以下任意次数(可能为 0)的操作来打印使该数组所有元素相等所需的最小步数。

*   **操作-1:** 选择任意前缀 **arr[1…k]** ，使得 max (arr[1]，arr[2]，…，arr[k]) = arr[k]，并为范围 **[1，k-1]**中的所有 **i** 设置 **arr[i] = arr[k]** 。
*   **操作-2:** 选择任意线段[L，R]并循环向左移动线段，保持其他元素不变。

**示例:**

> **输入:** arr[] = {1，2，12，20，18，19}
> **输出:** 2
> **解释:**分两步求解:
> 第一步，选择 L = 4 和 R = 6 应用操作 2，得到序列{1，2，12，18，19，20}。
> 第二步，对前缀 arr{1，2，12，18，19，20}应用操作 1，将 arr 转换为{20，20，20，20，20}，其中所有元素都相等。
> 
> **输入:** arr[] = {2，2，2，2}
> **输出:** 0
> **说明:**数组中的元素都是一样的。

**方法:**给定的问题可以通过使用以下观察来解决:

*   如果所有元素都相同，则无需进行任何操作。
*   如果数组的最大值最终是，那么仅对整个数组执行操作 1 会使所有元素相等。
*   如果最大值在最后一个位置之前，比如 j。然后在段[j，N]中执行操作 2，在那个操作 1 之后，前缀[1，N]使所有元素相等。

所以基于以上观察，答案可以是 0、1 或 2。遵循下面提到的步骤。

*   迭代数组并从数组中找到最大值。
*   如果数组的所有元素都相同，则返回 0。
*   如果最大值出现在数组的末尾，那么如观察结果所示，答案是 1。
*   如果这两个不是这样，那么答案是 2。

下面是上述方法的实现:

## C++

```
// C++ code to implement the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the minimum number
// of steps required to make all
// the elements are equal
void solve(int arr[], int N)
{
    // Initially assume all elements
    // are equal
    bool isEqual = true;

    // For finding the largest element
    int maxi = arr[0];

    // Loop to iterate through the array
    for (int i = 1; i < N; i++) {

        // If any element is not equal
        // than previous element, mark
        // it as false
        if (arr[i] != arr[i - 1]) {
            isEqual = false;
        }

        // Storing greater element
        maxi = max(maxi, arr[i]);
    }

    // If all the elements are equal
    if (isEqual) {
        cout << "0";
    }

    // If max element is found
    // at the last index
    else if (maxi == arr[N - 1]) {
        cout << "1";
    }

    // If max element is found
    // other than the last index
    else {
        cout << "2";
    }
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 12, 20, 18, 19 };
    int N = sizeof(arr) / sizeof(arr[0]);
    solve(arr, N);
    return 0;
}
```

## 蟒蛇 3

```
# Python3 code to implement the above approach

# Function to print the minimum number
# of steps required to make all
# the elements are equal
def solve(arr, N):

    # Initially assume all elements
    # are equal
    isEqual = True

    # For finding the largest element
    maxi = arr[0]

    # Loop to iterate through the array
    for i in range(1, N):

        # If any element is not equal
        # than previous element, mark
        # it as false
        if (arr[i] != arr[i - 1]):
            isEqual = False

        # Storing greater element
        maxi = max(maxi, arr[i])

    # If all the elements are equal
    if (isEqual):
        print("0")

    # If max element is found
    # at the last index
    elif (maxi == arr[N - 1]):
        print("1")

    # If max element is found
    # other than the last index
    else:
        print("2")

# Driver Code
if __name__=="__main__":

    arr = [ 1, 2, 12, 20, 18, 19 ]
    N = len(arr)

    solve(arr, N)

# This code is contributed by Akash Jha
```

**Output**

```
2
```

***时间复杂度:*** O(N)
***辅助空间:*** O(1)