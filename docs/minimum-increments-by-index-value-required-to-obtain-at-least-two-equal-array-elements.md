# 获得至少两个相等数组元素所需的索引值的最小增量

> 原文:[https://www . geeksforgeeks . org/按索引值最小增量-需要获得至少两个相等的数组元素/](https://www.geeksforgeeks.org/minimum-increments-by-index-value-required-to-obtain-at-least-two-equal-array-elements/)

给定由 **N** 个整数组成的严格递减数组 **arr[]** ，任务是找到使至少两个数组元素相等所需的最小操作数，其中每个操作都涉及将每个数组元素增加其索引值。

**示例:**

> **输入:** arr[] = {6，5，1}
> **输出:** 1
> **解释:**
> {6 + 1，5 + 2，1 + 3} = {7，7，4}
> **输入:** arr[] = {12，8，4}
> **输出:** 4
> **解释:**
> 步骤 1 : {12 + 1，8

**天真的做法:**按照以下步骤解决问题:

*   检查数组是否已经有至少两个相等的元素。如果发现是真的，打印 **0** 。
*   否则，通过将每个数组元素增加其索引值并增加**计数**来继续更新数组。检查数组是否有两个相等的元素。
*   一旦发现数组包含至少两个相等的元素，打印**计数**。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to update every element
// adding to it its index value
void update(int arr[], int N)
{
    for (int i = 0; i < N; i++) {
        arr[i] += (i + 1);
    }
}

// Function to check if at least
// two elements are equal or not
bool check(int arr[], int N)
{
    bool f = 0;
    for (int i = 0; i < N; i++) {

        // Count the frequency of arr[i]
        int count = 0;
        for (int j = 0; j < N; j++) {

            if (arr[i] == arr[j]) {
                count++;
            }
        }

        if (count >= 2) {
            f = 1;
            break;
        }
    }
    if (f == 1)
        return true;
    else
        return false;
}

// Function to calculate the number
// of increment operations required
void incrementCount(int arr[], int N)
{
    // Stores the minimum number of steps
    int min = 0;

    while (check(arr, N) != true) {
        update(arr, N);
        min++;
    }

    cout << min;
}

// Driver Code
int main()
{
    int N = 3;

    int arr[N] = { 12, 8, 4 };

    incrementCount(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to update every element
// adding to it its index value
static void update(int arr[], int N)
{
    for(int i = 0; i < N; i++)
    {
        arr[i] += (i + 1);
    }
}

// Function to check if at least
// two elements are equal or not
static boolean check(int arr[], int N)
{
    int f = 0;
    for(int i = 0; i < N; i++)
    {

        // Count the frequency of arr[i]
        int count = 0;
        for(int j = 0; j < N; j++)
        {
            if (arr[i] == arr[j])
            {
                count++;
            }
        }

        if (count >= 2)
        {
            f = 1;
            break;
        }
    }
    if (f == 1)
        return true;
    else
        return false;
}

// Function to calculate the number
// of increment operations required
static void incrementCount(int arr[], int N)
{

    // Stores the minimum number of steps
    int min = 0;

    while (check(arr, N) != true)
    {
        update(arr, N);
        min++;
    }
    System.out.println(min);
}

// Driver code
public static void main (String[] args)
{
    int N = 3;
    int arr[] = { 12, 8, 4 };

    incrementCount(arr, N);
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to update every element
# adding to it its index value
def update(arr, N):

    for i in range(N):
        arr[i] += (i + 1);

# Function to check if at least
# two elements are equal or not
def check(arr, N):

    f = 0;
    for i in range(N):

        # Count the frequency of arr[i]
        count = 0;

        for j in range(N):
            if (arr[i] == arr[j]):
                count += 1;

        if (count >= 2):
            f = 1;
            break;

    if (f == 1):
        return True;
    else:
        return False;

# Function to calculate the number
# of increment operations required
def incrementCount(arr, N):

    # Stores the minimum number of steps
    min = 0;

    while (check(arr, N) != True):
        update(arr, N);
        min += 1;

    print(min);

# Driver code
if __name__ == '__main__':

    N = 3;
    arr = [ 12, 8, 4 ];

    incrementCount(arr, N);

# This code is contributed by 29AjayKumar
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to update every element
// adding to it its index value
static void update(int []arr, int N)
{
    for(int i = 0; i < N; i++)
    {
        arr[i] += (i + 1);
    }
}

// Function to check if at least
// two elements are equal or not
static bool check(int []arr, int N)
{
    int f = 0;
    for(int i = 0; i < N; i++)
    {

        // Count the frequency of arr[i]
        int count = 0;
        for(int j = 0; j < N; j++)
        {
            if (arr[i] == arr[j])
            {
                count++;
            }
        }

        if (count >= 2)
        {
            f = 1;
            break;
        }
    }
    if (f == 1)
        return true;
    else
        return false;
}

// Function to calculate the number
// of increment operations required
static void incrementCount(int []arr, int N)
{

    // Stores the minimum number of steps
    int min = 0;

    while (check(arr, N) != true)
    {
        update(arr, N);
        min++;
    }
    Console.WriteLine(min);
}

// Driver code
public static void Main(String[] args)
{
    int N = 3;
    int []arr = { 12, 8, 4 };

    incrementCount(arr, N);
}
}

// This code is contributed by Amit Katiyar
```

## java 描述语言

```
<script>

// Java Script program to implement
// the above approach

// Function to update every element
// adding to it its index value
function update(arr,N)
{
    for(let i = 0; i < N; i++)
    {
        arr[i] += (i + 1);
    }
}

// Function to check if at least
// two elements are equal or not
function check(arr,N)
{
    let f = 0;
    for(let i = 0; i < N; i++)
    {

        // Count the frequency of arr[i]
        let count = 0;
        for(let j = 0; j < N; j++)
        {
            if (arr[i] == arr[j])
            {
                count++;
            }
        }

        if (count >= 2)
        {
            f = 1;
            break;
        }
    }
    if (f == 1)
        return true;
    else
        return false;
}

// Function to calculate the number
// of increment operations required
function incrementCount(arr,N)
{

    // Stores the minimum number of steps
    let min = 0;

    while (check(arr, N) != true)
    {
        update(arr, N);
        min++;
    }
    document.write(min);
}

// Driver code

    let N = 3;
    let arr= [12, 8, 4 ];

    incrementCount(arr, N);

//contributed by 171fa07058
</script>
```

**Output:** 

```
4
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)*

**有效方法:**上述方法可以通过观察到通过给定的操作，任意两个相邻元素之间的差随着阵列的减小而减小 1 来优化。因此，所需的最小操作数等于任意两个相邻元素之间的最小差值。

下面是上述方法的实现:

## C++

```
// C++ Program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate the minimum
// number of steps required
void incrementCount(int arr[], int N)
{
    // Stores minimum difference
    int mini = arr[0] - arr[1];

    for (int i = 2; i < N; i++) {

        mini
            = min(mini, arr[i - 1] - arr[i]);
    }

    cout << mini;
}

// Driver Code
int main()
{
    int N = 3;
    int arr[N] = { 12, 8, 4 };
    incrementCount(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;

class GFG{

// Function to calculate the minimum
// number of steps required
static void incrementCount(int arr[], int N)
{

    // Stores minimum difference
    int mini = arr[0] - arr[1];

    for(int i = 2; i < N; i++)
    {
        mini = Math.min(mini,
                        arr[i - 1] - arr[i]);
    }
    System.out.println(mini);
}   

// Driver code
public static void main (String[] args)
{
    int N = 3;
    int arr[] = { 12, 8, 4 };

    incrementCount(arr, N);
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to calculate the minimum
# number of steps required
def incrementCount(arr, N):

    # Stores minimum difference
    mini = arr[0] - arr[1]

    for i in range(2, N):
        mini = min(mini,
                   arr[i - 1] - arr[i])

    print(mini)

# Driver Code
N = 3
arr = [ 12, 8, 4 ]

# Function call
incrementCount(arr, N)

# This code is contributed by Shivam Singh
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to calculate the minimum
// number of steps required
static void incrementCount(int []arr, int N)
{

    // Stores minimum difference
    int mini = arr[0] - arr[1];

    for(int i = 2; i < N; i++)
    {
        mini = Math.Min(mini,
                        arr[i - 1] - arr[i]);
    }
    Console.WriteLine(mini);
}    

// Driver code
public static void Main(String[] args)
{
    int N = 3;
    int []arr = { 12, 8, 4 };

    incrementCount(arr, N);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program for the above approach

// Function to calculate the minimum
// number of steps required
function incrementCount(arr, N)
{

    // Stores minimum difference
    let mini = arr[0] - arr[1];

    for(let i = 2; i < N; i++)
    {
        mini = Math.min(mini,
                        arr[i - 1] - arr[i]);
    }
    document.write(mini);
}

// Driver Code

    let N = 3;
    let arr = [ 12, 8, 4 ];

    incrementCount(arr, N);

</script>
```

**Output:** 

```
4
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)