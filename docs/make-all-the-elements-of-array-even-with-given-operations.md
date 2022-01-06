# 用给定的操作使数组的所有元素均匀

> 原文:[https://www . geesforgeks . org/make-all-of-elements-of-array-even-with-given-operations/](https://www.geeksforgeeks.org/make-all-the-elements-of-array-even-with-given-operations/)

给定一个正整数的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** ，找到使所有[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)元素均匀分布所需的最小运算次数:

1.  如果有一个奇数，则将元素和下一个相邻元素递增 1。
2.  每次增量需要一次操作。

**注意:**如果**arr【】**中有任何数字在所有操作后都是奇数，那么，打印-1。

**示例:**

> **输入:** arr[] = {2，3，4，5，6}
> **输出:** 4
> **解释:**
> 加 1 至 3(在第一个索引处)，并在其相邻的元素 4(第二个索引处)上加 1。
> 现在数组变成了{2，4，5，5，6}。
> 将 1 添加到 5(在第二个索引处)，并将 1 添加到与其相邻的元素 5(第三个索引处)。
> 现在数组变成了{2，4，6，6，6}。
> 得到的数组都是偶数。
> 4 次增量的操作总数为 4。
> 
> **输入:** arr[] = {5，6}
> **输出:** -1
> **解释:**
> 加 1 到 5(第 0 个索引)，那么我们必须对其相邻的元素 6(第 1 个索引)增加 1。
> 现在数组变成了{6，7}。
> 在所有可能的增量之后，我们还有 1 个奇数。因此，我们不能使所有数组元素均匀。

**进场:**
这个问题可以用[贪婪进场](https://www.geeksforgeeks.org/greedy-algorithms/)解决。以下是步骤:

1.  遍历给定的[阵](https://www.geeksforgeeks.org/introduction-to-arrays/)T2【arr】。
2.  如果出现奇数元素，则将该元素增加 1，使其为偶数，并将下一个相邻元素增加 1。
3.  对给定的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** 的所有奇数元素重复上述步骤。
4.  如果**arr【】**中的所有元素都是偶数，那么打印操作数。
5.  否则打印-1。

下面是上述方法的实现:

## C++

```
// C++ program to make all array
// element even
#include "bits/stdc++.h"
using namespace std;

// Function to count the total
// number of operations needed to make
// all array element even
int countOperations(int arr[], int n)
{
    int count = 0;

    // Traverse the given array
    for (int i = 0; i < n - 1; i++) {

        // If an odd element occurs
        // then increment that element
        // and next adjacent element
        // by 1
        if (arr[i] & 1) {
            arr[i]++;
            arr[i + 1]++;
            count += 2;
        }
    }

    // Traverse the array if any odd
    // element occurs then return -1
    for (int i = 0; i < n; i++) {
        if (arr[i] & 1)
            return -1;
    }

    // Returns the count of operations
    return count;
}

int main()
{
    int arr[] = { 2, 3, 4, 5, 6 };
    int n = sizeof(arr) / sizeof(int);
    cout << countOperations(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to make all array
// element even
class GFG
{

// Function to count the total
// number of operations needed to make
// all array element even
static int countOperations(int arr[], int n)
{
    int count = 0;

    // Traverse the given array
    for (int i = 0; i < n - 1; i++)
    {

        // If an odd element occurs
        // then increment that element
        // and next adjacent element
        // by 1
        if (arr[i] % 2 == 1)
        {
            arr[i]++;
            arr[i + 1]++;
            count += 2;
        }
    }

    // Traverse the array if any odd
    // element occurs then return -1
    for (int i = 0; i < n; i++)
    {
        if (arr[i] % 2 == 1)
            return -1;
    }

    // Returns the count of operations
    return count;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 2, 3, 4, 5, 6 };
    int n = arr.length;
    System.out.print(countOperations(arr, n));
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to make all array
# element even

# Function to count the total
# number of operations needed to make
# all array element even
def countOperations(arr, n) :

    count = 0;

    # Traverse the given array
    for i in range(n - 1) :

        # If an odd element occurs
        # then increment that element
        # and next adjacent element
        # by 1
        if (arr[i] & 1) :
            arr[i] += 1;
            arr[i + 1] += 1;
            count += 2;

    # Traverse the array if any odd
    # element occurs then return -1
    for i in range(n) :
        if (arr[i] & 1) :
            return -1;

    # Returns the count of operations
    return count;

if __name__ == "__main__" :

    arr = [ 2, 3, 4, 5, 6 ];
    n = len(arr);
    print(countOperations(arr, n));

    # This code is contributed by AnkitRai01
```

## C#

```
// C# program to make all array
// element even
using System;

class GFG
{

// Function to count the total
// number of operations needed to make
// all array element even
static int countOperations(int []arr, int n)
{
    int count = 0;

    // Traverse the given array
    for (int i = 0; i < n - 1; i++)
    {

        // If an odd element occurs
        // then increment that element
        // and next adjacent element
        // by 1
        if (arr[i] % 2 == 1)
        {
            arr[i]++;
            arr[i + 1]++;
            count += 2;
        }
    }

    // Traverse the array if any odd
    // element occurs then return -1
    for (int i = 0; i < n; i++)
    {
        if (arr[i] % 2 == 1)
            return -1;
    }

    // Returns the count of operations
    return count;
}

// Driver code
public static void Main()
{
    int []arr = { 2, 3, 4, 5, 6 };
    int n = arr.Length;
    Console.Write(countOperations(arr, n));
}
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
// Javascript program to make all array
// element even

// Function to count the total
// number of operations needed to make
// all array element even
function countOperations(arr, n)
{
    let count = 0;

    // Traverse the given array
    for (let i = 0; i < n - 1; i++) {

        // If an odd element occurs
        // then increment that element
        // and next adjacent element
        // by 1
        if (arr[i] & 1) {
            arr[i]++;
            arr[i + 1]++;
            count += 2;
        }
    }

    // Traverse the array if any odd
    // element occurs then return -1
    for (let i = 0; i < n; i++) {
        if (arr[i] & 1)
            return -1;
    }

    // Returns the count of operations
    return count;
}

let arr = [ 2, 3, 4, 5, 6 ];
let n = arr.length;
document.write(countOperations(arr, n));

// This code is contributed by _saurabh_jaiswal
</script>
```

**Output:** 

```
4
```

**时间复杂度:** O(N)，其中 N 为数组中的元素个数。