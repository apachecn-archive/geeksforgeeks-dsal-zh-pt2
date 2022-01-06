# 检查一个数字是否是完美立方体的 C 程序

> 原文:[https://www . geesforgeks . org/c-program-to-check-number-is-perfect-cube-or-not/](https://www.geeksforgeeks.org/c-program-to-check-whether-a-number-is-a-perfect-cube-or-not/)

给定一个数字 **N** ，任务是编写 [C 程序](https://www.geeksforgeeks.org/c-programming-language/)检查给定的[数字是否是完美立方体](https://www.geeksforgeeks.org/perfect-cube/)。

**例:**

> ***输入:** N = 216*
> ***输出:** Yes*
> ***解释:***
> *As 216 = 6*6*6。
> 因此 216 的立方根是 6。*
> 
> ***输入:** N = 100*
> ***输出:**否*

**方法一:天真法**求给定数的立方根迭代从 **1** 到 **N** 的所有[自然数](https://www.geeksforgeeks.org/natural-numbers/)，检查该范围内任意数的立方是否等于给定数 **N** ，然后打印**是**否则打印**否**

下面是上述方法的实现:

## C

```
// C program for the above approach
#include <math.h>
#include <stdio.h>

// Function to check if a number is
// a perfect Cube
void perfectCube(int N)
{
    for (int i = 1; i < N; i++) {

        // If cube of i is equals to N
        // then print Yes and return
        if (i * i * i == N) {
            printf("Yes");
            return;
        }
    }

    // No number was found whose cube
    // is equal to N
    printf("No");
    return;
}

// Driver Code
int main()
{
    // Given Number
    int N = 216;

    // Function Call
    perfectCube(N);
    return 0;
}
```

**Output:**

```
Yes

```

**复杂度分析:**

*   **时间复杂度:** O(N)，只需要对解进行一次遍历，因此时间复杂度为 O(N)。
*   **辅助空间:** O(1)。需要恒定的额外空间。

**方法二:使用内置函数**思路是使用内置函数 [pow()](https://www.geeksforgeeks.org/power-function-cc/) 求一个数的立方根，该数返回该数立方根的 [楼层值](https://www.geeksforgeeks.org/ceil-floor-functions-cpp/)**N**。如果这个数的立方等于 **N** ，那么 **N** 就是一个完美的立方，否则 **N** 就不是一个完美的立方。

下面是上述方法的实现:

## C

```
// C program for the above approach
#include <math.h>
#include <stdio.h>

// Function to check if a number is
// perfect cube using inbuilt function
void perfectCube(int N)
{
    int cube_root;
    cube_root = (int)round(pow(N, 1.0 / 3.0));

    // If cube of cube_root is equals
    // to N, then print Yes else No
    if (cube_root * cube_root * cube_root == N) {
        printf("Yes");
        return;
    }
    else {
        printf("No");
        return;
    }
}

// Driver Code
int main()
{
    // Given number N
    int N = 216;

    // Function Call
    perfectCube(N);
    return 0;
}
```

**Output:**

```
Yes

```

**复杂度分析:**

*   **时间复杂度:** O(N)，由于 pow()函数在 O(N)中工作，所以时间复杂度为 O(N)。
*   **辅助空间:** O(1)。需要恒定的额外空间。

**方法三:用二分搜索法**思路是用[二分搜索法](http://geeksquiz.com/binary-search/) 解决问题。 *i * i * i* 的值是单调递增的，所以这个问题可以用二分搜索法来解决。
以下是步骤:

1.  Initialize **low and** high to **0 and n** respectively.
2.  Iterate to low ≤ high, and do the following:
    *   Find the median value of **as = (low+high)/2** .
    *   Check whether **middle * middle * middle** is equal to **n** , and then print **Yes** .
    *   If the cube of mid is less than **n** , then search for a larger value in the second half of the search space by updating as low as mid+1.
    *   If the cube of mid is greater than **n** , search for a smaller value in the first half of the search space by updating high to mid–1.
3.  If the cube of n is not obtained in the above step, print **No** .

下面是上述方法的实现:

## C

```
// C program for the above approach
#include <math.h>
#include <stdio.h>

// Function to check if a number is
// a perfect Cube using binary search
void perfectCube(int N)
{
    int start = 1, end = N;
    while (start <= end) {

        // Calculating mid
        int mid = (start + end) / 2;

        // If N is a perfect cube
        if (mid * mid * mid == N) {
            printf("Yes");
            return;
        }

        // If mid^3 is smaller than N,
        // then move closer to cube
        // root of N
        if (mid * mid * mid < N) {
            start = mid + 1;
        }

        // If mid^3 is greater than N
        else
            end = mid - 1;
    }

    printf("No");
    return;
}

// Driver Code
int main()
{
    // Given Number N
    int N = 216;

    // Function Call
    perfectCube(N);
    return 0;
}
```

**输出:**

```
Yes

```

**复杂度分析:**

*   **时间复杂度:** O(对数 N)。二分搜索法的时间复杂度为 0(对数 N)。
*   **辅助空间:** O(1)。需要恒定的额外空间。