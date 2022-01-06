# 找到所有比右边所有元素都小的数组元素

> 原文:[https://www . geesforgeks . org/find-all-array-元素-比所有元素都要小的元素-它们的右边/](https://www.geeksforgeeks.org/find-all-array-elements-that-are-smaller-than-all-elements-to-their-right/)

给定一个包含正整数 **N** 的数组 **arr[]** 。任务是找到所有比右边的元素小的元素。

**示例:**

> **输入:** arr[] = {6，14，13，21，17，19}
> **输出:**【6，13，17，19】
> **说明:**输出中的所有元素都遵循条件。
> 
> **输入:** arr[] = {10，3，4，8，7}
> **输出:**【3，4，7】

**天真方法:**这种方法使用两个循环。对于每个元素，遍历其右侧的数组，并检查是否存在任何较小的元素。如果数组右边的所有元素都大于它，那么打印这个元素。

***时间复杂度:*** O(N*N)
***辅助空间:*** O(1)

**高效方法:**在高效方法中，思路是使用[栈](https://www.geeksforgeeks.org/stack-data-structure/)。遵循以下步骤:

*   从数组的开头迭代数组。
*   对于数组中的每个元素，弹出堆栈中所有大于它的元素，然后将其推入堆栈。
*   如果没有大于它的元素，那么当前元素就是答案。
*   最后，堆栈保留了比其右侧所有元素都小的元素。

下面是上述方法的代码实现。

## C++

```
// C++ program to find all elements in array
// that are smaller than all elements
// to their right.
#include <iostream>
#include <stack>
#include <vector>
using namespace std;

// Function to print all elements which are
// smaller than all elements present
// to their right
void FindDesiredElements(vector<int> const& arr)
{
    // Create an empty stack
    stack<int> stk;

    // Do for each element
    for (int i : arr) {
        // Pop all the elements that
        // are greater than the
        // current element
        while (!stk.empty() && stk.top() > i) {
            stk.pop();
        }

        // Push current element into the stack
        stk.push(i);
    }

    // Print all elements in the stack
    while (!stk.empty()) {
        cout << stk.top() << " ";
        stk.pop();
    }
}

// Driver Code
int main()
{
    vector<int> arr = { 6, 14, 13, 21, 17, 19 };

    FindDesiredElements(arr);
    return 0;
}
```

**Output**

```
19 17 13 6 
```

***时间复杂度:*** O(N)
***辅助空间:*** O(N)

**空间优化方法:**想法是从右向左遍历数组(逆序)，并维护一个辅助变量，存储到目前为止找到的最小元素。这种方法会忽略堆栈的使用。请遵循以下步骤:

*   从数组末尾开始迭代。
*   如果当前元素小于迄今为止的最小值，则找到该元素。更新目前为止存储最小值的值。打印所有这些值作为答案。

下面是上述方法的实现。

## C++

```
// C++ program to print all elements which are
// smaller than all elements present to their right

#include <iostream>
#include <limits.h>
using namespace std;

// Function to print all elements which are
// smaller than all elements
// present to their right
void FindDesiredElements(int arr[], int n)
{
    int min_so_far = INT_MAX;

    // Traverse the array from right to left
    for (int j = n - 1; j >= 0; j--) {
        // If the current element is greater
        //  than the maximum so far, print it
        // and update `max_so_far`
        if (arr[j] <= min_so_far) {
            min_so_far = arr[j];
            cout << arr[j] << " ";
        }
    }
}

// Driver Code
int main()
{
    int arr[] = { 6, 14, 13, 21, 17, 19 };
    int N = sizeof(arr) / sizeof(arr[0]);

    FindDesiredElements(arr, N);
    return 0;
}
```

## java 描述语言

```
<script>
      // JavaScript code for the above approach

      // Function to print all elements which are
      // smaller than all elements
      // present to their right
      function FindDesiredElements(arr, n)
      {
          let min_so_far = Number.MAX_VALUE;

          // Traverse the array from right to left
          for (let j = n - 1; j >= 0; j--)
          {

              // If the current element is greater
              //  than the maximum so far, print it
              // and update `max_so_far`
              if (arr[j] <= min_so_far) {
                  min_so_far = arr[j];
                  document.write(arr[j] + " ");
              }
          }
      }

      // Driver Code
      let arr = [6, 14, 13, 21, 17, 19];
      let N = arr.length;

      FindDesiredElements(arr, N);

// This code is contributed by Potta Lokesh
  </script>
```

**Output**

```
19 17 13 6 
```

***时间复杂度:*** O(N)
***辅助空间:*** O(1)