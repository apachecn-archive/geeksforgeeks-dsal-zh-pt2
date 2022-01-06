# 数组中奇数和偶数对的计数

> 原文:[https://www . geesforgeks . org/数组中奇数和偶数对的计数/](https://www.geeksforgeeks.org/count-of-odd-and-even-sum-pairs-in-an-array/)

给定一个正整数数组**arr[]****N**，任务是求奇数和的对数以及偶数和的对数。
**例:**

> **输入:** arr[] = {1，2，3，4，5}
> **输出:**
> 奇数对= 6
> 偶数对= 4
> **输入:** arr[] = {7，4，3，2}
> **输出:**
> 奇数对= 4
> 偶数对= 2

**天真方法:**
这个问题的天真方法是遍历数组中的每一对元素，检查它们的和，然后计算具有奇数和偶数和的对的数量。这种方法需要 O(N*N)个时间。
**高效方法:**

*   计算数组中奇数和偶数元素的数量，并将其存储在变量**和**以及**和**中。
*   为了得到偶的对和，所有偶元素只与偶元素配对，所有奇元素只与奇元素配对，计数为**((cntevery *(cntevery–1))/2)+((cntOdd *(cntOdd–1))/2)**
*   现在，为了使总和为奇数，该对元素中的一个必须为偶数，另一个必须为奇数，并且所需的计数将为**CNT 偶数* CNT 奇数**。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the count of pairs
// with odd sum and the count
// of pairs with even sum
void findPairs(int arr[], int n)
{

    // To store the count of even and
    // odd number from the array
    int cntEven = 0, cntOdd = 0;

    for (int i = 0; i < n; i++) {

        // If the current element is even
        if (arr[i] % 2 == 0)
            cntEven++;

        // If it is odd
        else
            cntOdd++;
    }

    // To store the count of
    // pairs with even sum
    int evenPairs = 0;

    // All the even elements will make
    // pairs with each other and the
    // sum of the pair will be even
    evenPairs += ((cntEven * (cntEven - 1)) / 2);

    // All the odd elements will make
    // pairs with each other and the
    // sum of the pair will be even
    evenPairs += ((cntOdd * (cntOdd - 1)) / 2);

    // To store the count of
    // pairs with odd sum
    int oddPairs = 0;

    // All the even elements will make pairs
    // with all the odd element and the
    // sum of the pair will be odd
    oddPairs += (cntEven * cntOdd);

    cout << "Odd pairs = " << oddPairs << endl;
    cout << "Even pairs = " << evenPairs;
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 3, 4, 5 };
    int n = sizeof(arr) / sizeof(int);

    findPairs(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to find the count of pairs
// with odd sum and the count
// of pairs with even sum
static void findPairs(int arr[], int n)
{

    // To store the count of even and
    // odd number from the array
    int cntEven = 0, cntOdd = 0;

    for (int i = 0; i < n; i++)
    {

        // If the current element is even
        if (arr[i] % 2 == 0)
            cntEven++;

        // If it is odd
        else
            cntOdd++;
    }

    // To store the count of
    // pairs with even sum
    int evenPairs = 0;

    // All the even elements will make
    // pairs with each other and the
    // sum of the pair will be even
    evenPairs += ((cntEven * (cntEven - 1)) / 2);

    // All the odd elements will make
    // pairs with each other and the
    // sum of the pair will be even
    evenPairs += ((cntOdd * (cntOdd - 1)) / 2);

    // To store the count of
    // pairs with odd sum
    int oddPairs = 0;

    // All the even elements will make pairs
    // with all the odd element and the
    // sum of the pair will be odd
    oddPairs += (cntEven * cntOdd);

    System.out.println("Odd pairs = " + oddPairs);
    System.out.println("Even pairs = " + evenPairs);
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 1, 2, 3, 4, 5 };
    int n = arr.length;

    findPairs(arr, n);
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to find the count of pairs
# with odd sum and the count
# of pairs with even sum
def findPairs(arr, n) :

    # To store the count of even and
    # odd number from the array
    cntEven = 0; cntOdd = 0;

    for i in range(n) :

        # If the current element is even
        if (arr[i] % 2 == 0) :
            cntEven += 1;

        # If it is odd
        else :
            cntOdd += 1;

    # To store the count of
    # pairs with even sum
    evenPairs = 0;

    # All the even elements will make
    # pairs with each other and the
    # sum of the pair will be even
    evenPairs += ((cntEven * (cntEven - 1)) // 2);

    # All the odd elements will make
    # pairs with each other and the
    # sum of the pair will be even
    evenPairs += ((cntOdd * (cntOdd - 1)) // 2);

    # To store the count of
    # pairs with odd sum
    oddPairs = 0;

    # All the even elements will make pairs
    # with all the odd element and the
    # sum of the pair will be odd
    oddPairs += (cntEven * cntOdd);

    print("Odd pairs = ", oddPairs);
    print("Even pairs = ", evenPairs);

# Driver code
if __name__ == "__main__" :

    arr = [ 1, 2, 3, 4, 5 ];
    n = len(arr);

    findPairs(arr, n);

# This code is contributed by kanugargng
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to find the count of pairs
// with odd sum and the count
// of pairs with even sum
static void findPairs(int []arr, int n)
{

    // To store the count of even and
    // odd number from the array
    int cntEven = 0, cntOdd = 0;

    for (int i = 0; i < n; i++)
    {

        // If the current element is even
        if (arr[i] % 2 == 0)
            cntEven++;

        // If it is odd
        else
            cntOdd++;
    }

    // To store the count of
    // pairs with even sum
    int evenPairs = 0;

    // All the even elements will make
    // pairs with each other and the
    // sum of the pair will be even
    evenPairs += ((cntEven * (cntEven - 1)) / 2);

    // All the odd elements will make
    // pairs with each other and the
    // sum of the pair will be even
    evenPairs += ((cntOdd * (cntOdd - 1)) / 2);

    // To store the count of
    // pairs with odd sum
    int oddPairs = 0;

    // All the even elements will make pairs
    // with all the odd element and the
    // sum of the pair will be odd
    oddPairs += (cntEven * cntOdd);

    Console.WriteLine("Odd pairs = " + oddPairs);
    Console.WriteLine("Even pairs = " + evenPairs);
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 1, 2, 3, 4, 5 };
    int n = arr.Length;

    findPairs(arr, n);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function to find the count of pairs
// with odd sum and the count
// of pairs with even sum
function findPairs(arr, n) {

    // To store the count of even and
    // odd number from the array
    let cntEven = 0, cntOdd = 0;

    for (let i = 0; i < n; i++) {

        // If the current element is even
        if (arr[i] % 2 == 0)
            cntEven++;

        // If it is odd
        else
            cntOdd++;
    }

    // To store the count of
    // pairs with even sum
    let evenPairs = 0;

    // All the even elements will make
    // pairs with each other and the
    // sum of the pair will be even
    evenPairs += ((cntEven * (cntEven - 1)) / 2);

    // All the odd elements will make
    // pairs with each other and the
    // sum of the pair will be even
    evenPairs += ((cntOdd * (cntOdd - 1)) / 2);

    // To store the count of
    // pairs with odd sum
    let oddPairs = 0;

    // All the even elements will make pairs
    // with all the odd element and the
    // sum of the pair will be odd
    oddPairs += (cntEven * cntOdd);

    document.write("Odd pairs = " + oddPairs + "<br>");
    document.write("Even pairs = " + evenPairs);
}

// Driver code
let arr = [1, 2, 3, 4, 5];
let n = arr.length;

findPairs(arr, n);

// This code is contributed by _saurabh_jaiswal
</script>
```

**Output:** 

```
Odd pairs = 6
Even pairs = 4
```

**<u>复杂度分析:</u>**

*   **时间复杂度:** O(N)。
    在 for 循环的每一次迭代中，都会处理任一数组中的元素。因此，时间复杂度为 O(N)。
*   **辅助空间:** O(1)。
    不需要任何额外的空间，所以空间复杂度不变。