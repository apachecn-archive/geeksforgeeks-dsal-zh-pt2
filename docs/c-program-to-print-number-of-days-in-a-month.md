# C 程序打印一个月的天数

> 原文:[https://www . geesforgeks . org/c-程序转打印-月天数/](https://www.geeksforgeeks.org/c-program-to-print-number-of-days-in-a-month/)

给定一个数字 **N** ，任务是找出每个月对应的天数，其中 1 是 1 月，2 是 2 月，3 是 3 月，依此类推。

**示例:**

> **输入:**N = 12
> T3】输出: 31 天
> 
> **输入:**N = 2
> T3】输出: 28/29 天

**方法–1:使用 [If Else](https://www.geeksforgeeks.org/decision-making-c-c-else-nested-else/) :**

1.  将输入的月份作为数字 **N** 获取。
2.  如果 N 是这些值 1、3、5、7、8、10、12 中的一个，则打印**“31 天”**。
3.  如果 N 是这些值 4、6、9、11 中的一个，则打印**“30 天”**。
4.  如果 N 为 2，则打印**“28/29 天。”**。
5.  否则打印**“无效月”**。

下面是上述方法的实现:

```
// C program for the above approach
#include <stdio.h>

// Function to find the number of Days
// in month input by user
void printNumberOfDays(int N)
{

    // Check for 31 Days
    if (N == 1 || N == 3 || N == 5
        || N == 7 || N == 8 || N == 10
        || N == 12) {
        printf("31 Days.");
    }

    // Check for 30 Days
    else if (N == 4 || N == 6
             || N == 9 || N == 11) {
        printf("30 Days.");
    }

    // Check for 28/29 Days
    else if (N == 2) {
        printf("28/29 Days.");
    }

    // Else Invalid Input
    else {
        printf("Invalid Month.");
    }
}

// Driver Code
int main()
{
    // Input Month
    int N = 4;

    // Function Call
    printNumberOfDays(N);

    return 0;
}
```

**Output:**

```
30 Days.

```

***时间复杂度:** *O(1)*
**辅助空间:** *O(1)**

**方法 2:使用[开关语句](https://www.geeksforgeeks.org/switch-statement-cc/) :**

1.  将输入的月份作为数字 **N** 获取。
2.  当 N 值为 1、3、5、7、8、10、12 中的一个时，使用 switch 语句，然后打印**“31 天”**对应开关情况。
3.  如果 N 是这些值 4、6、9、11 中的一个，则打印**“30 天”**对应开关情况。
4.  如果 N 为 2，则打印**“28/29 天。”**对应开关情况。
5.  否则开关情况的默认条件将打印**“无效月”**。

下面是上述方法的实现:

```
// C program for the above approach
#include <stdio.h>

// Function to find the number of Days
// in month input by user usingwwww
// switch statement
void printNumberOfDays(int N)
{

    switch (N) {
    // Cases for 31 Days
    case 1:
    case 3:
    case 5:
    case 7:
    case 8:
    case 10:
    case 12:
        printf("31 Days.");
        break;

    // Cases for 30 Days
    case 4:
    case 6:
    case 9:
    case 11:
        printf("30 Days.");
        break;

    // Case for 28/29 Days
    case 2:
        printf("28/29 Days.");
        break;

    default:
        printf("Invalid Month.");
        break;
    }
}

// Driver Code
int main()
{
    // Input Month
    int N = 4;

    // Function Call
    printNumberOfDays(N);

    return 0;
}
```

**Output:**

```
30 Days.

```

***时间复杂度:** *O(1)*
**辅助空间:** *O(1)**

**方法–3:使用[阵列](https://www.geeksforgeeks.org/arrays-in-c-cpp/) :**

1.  将每个月对应的天数值存储为数组:

    > arr[12] = { 31，28，31，30，31，30，31，30，31，31，31，31，30，31 }

2.  从上面的数组中打印每个月的相应日期。

下面是上述方法的实现:

```
// C program to find the number of days
// in a month using arrays
#include <stdio.h>

// Driver Code
int main()
{
    // Store the day in array arr[]
    int arr[12] = { 31, 28, 31, 30, 31, 30,
                    31, 31, 30, 31, 30, 31 };

    // Input Month
    int N = 4;

    // Print the number of days in
    // month 4
    printf("%d Days.", arr[N - 1]);

    return 0;
}
```

**Output:**

```
30 Days.

```

**时间复杂度:***O(1)*
T5】辅助空间: *O(1)*

**方法–4:使用[指针](https://www.geeksforgeeks.org/pointers-in-c-and-c-set-1-introduction-arithmetic-and-array/) :**

1.  将每个月对应的天数值存储为数组:

    > arr[12] = { 31，28，31，30，31，30，31，30，31，31，31，31，30，31 }

2.  使用指针从上面的数组中打印每个月的相应日期，如下所示:

    > printf("%d 天“，*(arr+(* N–1)))

下面是上述方法的实现:

```
// C program to find the number of days
// in a month using pointers
#include <stdio.h>

// Function to print number of Days
void printNumberOfDays(int* arr, int* N)
{
    // Print the number of days for Nth
    // month using *(arr+(*N - 1))
    printf("%d Days.", *(arr + (*N - 1)));
}

// Driver Code
int main()
{
    // Store the day in array arr[]
    int arr[12] = { 31, 28, 31, 30, 31, 30,
                    31, 31, 30, 31, 30, 31 };

    // Input Month
    int N = 4;

    // Print the number of days in
    // month 4
    printNumberOfDays(arr, &N);

    return 0;
}
```

**Output:**

```
30 Days.

```

***时间复杂度:** *O(1)*
**辅助空间:** *O(1)**