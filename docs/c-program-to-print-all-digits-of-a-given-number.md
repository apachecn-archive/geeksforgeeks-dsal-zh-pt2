# C 程序打印给定数字的所有数字

> 原文:[https://www . geesforgeks . org/c-程序打印给定号码的所有数字/](https://www.geeksforgeeks.org/c-program-to-print-all-digits-of-a-given-number/)

给定一个数字 **N** ，任务是编写一个 C 程序，以原始顺序打印数字 **N** 的所有数字。

**示例:**

> **输入:**N = 12
> T3】输出: 1，2
> 
> **输入:**N = 1032
> T3】输出: 1，0，3，2

**方法一:**最简单的方法就是把数字一个个提取出来打印出来。

1.  通过 **N%10** 提取数字 **N** 的最后一位数字，并将该数字存储在数组中(比如 **arr[]** )。
2.  通过 **N/10** 更新 **N** 的值，重复上述步骤直到 **N** 不等于 **0** 。
3.  提取并存储所有数字后，从头到尾遍历数组并打印其中存储的数字。

下面是上述方法的实现:

```
// C program of the above approach

#include <stdio.h>
#define MAX 100

// Function to print the digit of
// number N
void printDigit(int N)
{
    // To store the digit
    // of the number N
    int arr[MAX];
    int i = 0;
    int j, r;

    // Till N becomes 0
    while (N != 0) {

        // Extract the last digit of N
        r = N % 10;

        // Put the digit in arr[]
        arr[i] = r;
        i++;

        // Update N to N/10 to extract
        // next last digit
        N = N / 10;
    }

    // Print the digit of N by traversing
    // arr[] reverse
    for (j = i - 1; j > -1; j--) {
        printf("%d ", arr[j]);
    }
}

// Driver Code
int main()
{
    int N = 3452897;

    printDigit(N);
    return 0;
}
```

**Output:**

```
3 4 5 2 8 9 7

```

***时间复杂度:** O(log <sub>10</sub> N)
**辅助空间:** O(log <sub>10</sub> N)*

**方法二:使用递归**

1.  递归迭代直到 N 变成 0:
    *   **基本情况:**如果 **N** 的值为 **0** ，则退出该功能。

        ```
        if(N==0) 
          return ;

        ```

    *   **递归调用:**如果不满足基本情况，递归调用下一次迭代，将 **N** 更新为 **N/10** 并打印递归调用后从数字 **N** 中提取的最后一位数字(比如 **r** )的值。

        ```
        recursive_function(N/10);
        print(r);

        ```

下面是上述方法的实现:

```
// C program of the above approach

#include <stdio.h>

// Function to print the digit of
// number N
void printDigit(int N)
{
    int r;

    // Base Case
    if (N == 0) {
        return;
    }

    // Extract the last digit
    r = N % 10;

    // Recursive call to next
    // iteration
    printDigit(N / 10);

    // Print r
    printf("%d ", r);
}

// Driver Code
int main()
{
    int N = 3452897;

    printDigit(N);
    return 0;
}
```

**Output:**

```
3 4 5 2 8 9 7

```

***时间复杂度:** O(log <sub>10</sub> N)
**辅助空间:** O(1)*