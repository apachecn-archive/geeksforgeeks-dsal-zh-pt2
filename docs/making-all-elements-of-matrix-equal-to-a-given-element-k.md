# 使矩阵的所有元素等于给定的元素 K

> 原文:[https://www . geeksforgeeks . org/making-所有矩阵元素等于给定元素-k/](https://www.geeksforgeeks.org/making-all-elements-of-matrix-equal-to-a-given-element-k/)

给定一个二维数组 **arr[][]** ，任务是检查是否有可能使数组的所有元素等于一个给定的数 **k** ，如果在一个操作中，可以选择任何元素并且周围的对角线元素可以等于它。
**例:**

```
Input:
arr[][] = 1 8 3
          1 2 2
          4 1 9
k = 2
Output: Yes
Explanation: 
In first operation choose element at (2, 2)
New array = 2 8 2
            1 2 2 
            2 1 2
In second operation choose element at (2, 3)
New array = 2 2 2
            1 2 2
            2 2 2 
In third operation choose element at (1, 2)
New array = 2 2 2 
            2 2 2 
            2 2 2

Input:
arr[][] = 3 1 2 3
          2 1 8 6
          9 7 9 9
k = 4 
Output:
No
```

**进场:**

*   矩阵可以认为是一个有黑白方块的棋盘。
*   如果选择了黑盒中等于给定数字的任何元素，则可以使用给定操作使黑盒的所有元素都等于它，
*   同样，可以检查白色方框。所以在黑盒和白盒中都需要至少有一个元素等于给定的元素。
*   所以我们需要使用计数器迭代所有元素。如果计数器的值是奇数，可以认为是黑盒，对于偶数，可以认为是白盒。

下面是上述方法的实现。

## C++

```
// C++ implementation of the above approach.
#include <iostream>
using namespace std;

// Function to check if all
// elements can be equal or not
void checkEqualMatrix(int arr[][3], int n,
                      int m, int k)
{
    int c = 0, cnt1 = 0, cnt2 = 0;

    // Iterate over the matrix
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < m; j++) {
            if (c % 2 == 0) {

                // Update the counter for odd values
                // if array element at that position is k
                if (arr[i][j] == k) {
                    cnt1++;
                }
            }
            else {

                // Update the counter for even values
                // if array element at that position is k
                if (arr[i][j] == k) {
                    cnt2++;
                }
            }
            c = c + 1;
        }
    }
    // To check if there is at least one
    // element at both even and odd indices.
    if (cnt1 >= 1 && cnt2 >= 1) {
        cout << "Yes";
    }
    else {
        cout << "No";
    }
}

// Driver code
int main()
{
    int arr[3][3] = { { 1, 8, 3 },
                      { 1, 2, 2 },
                      { 4, 1, 9 } };
    int k = 2;
    // Function calling
    checkEqualMatrix(arr, 3, 3, k);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach.
class GFG
{

    // Function to check if all
    // elements can be equal or not
    static void checkEqualMatrix(int arr[][], int n,
                              int m, int k)
    {
        int c = 0, cnt1 = 0, cnt2 = 0;

        // Iterate over the matrix
        for (int i = 0; i < n; i++)
        {
            for (int j = 0; j < m; j++)
            {
                if (c % 2 == 0)
                {

                    // Update the counter for odd values
                    // if array element at that position is k
                    if (arr[i][j] == k)
                    {
                        cnt1++;
                    }
                }
                else
                {

                    // Update the counter for even values
                    // if array element at that position is k
                    if (arr[i][j] == k)
                    {
                        cnt2++;
                    }
                }
                c = c + 1;
            }
        }

        // To check if there is at least one
        // element at both even and odd indices.
        if (cnt1 >= 1 && cnt2 >= 1)
        {
            System.out.println("Yes");
        }
        else
        {
            System.out.println("No");
        }
    }

    // Driver code
    public static void main (String[] args)
    {
        int arr[][] = { { 1, 8, 3 },
                        { 1, 2, 2 },
                        { 4, 1, 9 } };
        int k = 2;

        // Function calling
        checkEqualMatrix(arr, 3, 3, k);
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the above approach.

# Function to check if all
# elements can be equal or not
def checkEqualMatrix(arr, n, m, k) :

    c = 0; cnt1 = 0; cnt2 = 0;

    # Iterate over the matrix
    for i in range(n) :
        for j in range(m) :
            if (c % 2 == 0) :

                # Update the counter for odd values
                # if array element at that position is k
                if (arr[i][j] == k) :
                    cnt1 += 1;

            else :

                # Update the counter for even values
                # if array element at that position is k
                if (arr[i][j] == k) :
                    cnt2 += 1;

            c = c + 1;

    # To check if there is at least one
    # element at both even and odd indices.
    if (cnt1 >= 1 and cnt2 >= 1) :
        print("Yes");
    else :
        print("No");

# Driver code
if __name__ == "__main__" :

    arr = [
            [ 1, 8, 3 ],
            [ 1, 2, 2 ],
            [ 4, 1, 9 ]
            ];

    k = 2;

    # Function calling
    checkEqualMatrix(arr, 3, 3, k);

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the above approach.
using System;

class GFG
{

    // Function to check if all
    // elements can be equal or not
    static void checkEqualMatrix(int [,]arr, int n,
                                        int m, int k)
    {
        int c = 0, cnt1 = 0, cnt2 = 0;

        // Iterate over the matrix
        for (int i = 0; i < n; i++)
        {
            for (int j = 0; j < m; j++)
            {
                if (c % 2 == 0)
                {

                    // Update the counter for odd values
                    // if array element at that position is k
                    if (arr[i,j] == k)
                    {
                        cnt1++;
                    }
                }
                else
                {

                    // Update the counter for even values
                    // if array element at that position is k
                    if (arr[i,j] == k)
                    {
                        cnt2++;
                    }
                }
                c = c + 1;
            }
        }

        // To check if there is at least one
        // element at both even and odd indices.
        if (cnt1 >= 1 && cnt2 >= 1)
        {
            Console.WriteLine("Yes");
        }
        else
        {
            Console.WriteLine("No");
        }
    }

    // Driver code
    public static void Main()
    {
        int [,]arr = { { 1, 8, 3 },
                        { 1, 2, 2 },
                        { 4, 1, 9 } };
        int k = 2;

        // Function calling
        checkEqualMatrix(arr, 3, 3, k);
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach.

// Function to check if all
// elements can be equal or not
function checkEqualMatrix(arr, n, m, k)
{
    var c = 0, cnt1 = 0, cnt2 = 0;

    // Iterate over the matrix
    for (var i = 0; i < n; i++) {
        for (var j = 0; j < m; j++) {
            if (c % 2 == 0) {

                // Update the counter for odd values
                // if array element at that position is k
                if (arr[i][j] == k) {
                    cnt1++;
                }
            }
            else {

                // Update the counter for even values
                // if array element at that position is k
                if (arr[i][j] == k) {
                    cnt2++;
                }
            }
            c = c + 1;
        }
    }

    // To check if there is at least one
    // element at both even and odd indices.
    if (cnt1 >= 1 && cnt2 >= 1) {
        document.write( "Yes");
    }
    else {
        document.write( "No");
    }
}

// Driver code
var arr = [ [ 1, 8, 3 ],
                  [ 1, 2, 2 ],
                  [ 4, 1, 9 ] ];
var k = 2;

// Function calling
checkEqualMatrix(arr, 3, 3, k);

// This code is contributed by importantly.

</script>
```

**Output:** 

```
Yes
```