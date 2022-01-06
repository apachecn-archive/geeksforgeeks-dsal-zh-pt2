# 偶数索引处的偶数和奇数索引处的奇数

> 原文:[https://www . geesforgeks . org/偶数-偶数-索引-奇数-索引/](https://www.geeksforgeeks.org/even-numbers-even-index-odd-numbers-odd-index/)

给定一个大小为 **n** 的数组，其中包含相同数量的奇数和偶数。问题是排列数字的方式是所有的偶数得到偶数索引，奇数得到奇数索引。所需辅助空间为 0(1)。
**例:**

```
Input : arr[] = {3, 6, 12, 1, 5, 8}
Output : 6 3 12 1 8 5 

Input : arr[] = {10, 9, 7, 18, 13, 19, 4, 20, 21, 14}
Output : 10 9 18 7 20 19 4 13 14 21 
```

**来源:** [亚马逊面试体验|第 410 集。](https://www.geeksforgeeks.org/amazon-interview-experience-set-410-campus-internship/)

**进场:**

*   从左边开始，保留两个索引，一个用于偶数位置，另一个用于奇数位置。
*   从左边穿过这些索引。
*   偶数位置应该有偶数，奇数位置应该有奇数。
*   每当出现不匹配时，我们交换奇数和偶数索引处的值。

以下是上述方法的实现:

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ implementation to arrange
// odd and even numbers
#include <bits/stdc++.h>
using namespace std;

// function to arrange odd and even numbers
void arrangeOddAndEven(int arr[], int n)
{
   int oddInd = 1;
    int evenInd = 0;
    while (true)
    {
        while (evenInd < n && arr[evenInd] % 2 == 0)
            evenInd += 2;

        while (oddInd < n && arr[oddInd] % 2 == 1)
            oddInd += 2;

        if (evenInd < n && oddInd < n)
            swap (arr[evenInd], arr[oddInd]);

        else
            break;
    }
}

// function to print the array
void printArray(int arr[], int n)
{
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
}

// Driver program to test above
int main()
{
    int arr[] = { 3, 6, 12, 1, 5, 8 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << "Original Array: ";
    printArray(arr, n);

    arrangeOddAndEven(arr, n);

    cout << "\nModified Array: ";
    printArray(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to
// arrange odd and even numbers

import java.util.*;
import java.lang.*;

class GfG {

// function to arrange
// odd and even numbers
public static void arrangeOddAndEven(int arr[], int n)
{
    int oddInd = 1;
    int evenInd = 0;
    while (true)
    {
        while (evenInd < n && arr[evenInd] % 2 == 0)
            evenInd += 2;

        while (oddInd < n && arr[oddInd] % 2 == 1)
            oddInd += 2;

        if (evenInd < n && oddInd < n)
            {
                int temp = arr[evenInd];
                arr[evenInd] = arr[oddInd];
                arr[oddInd] = temp;
            }

        else
            break;
    }
}

// function to print the array
public static void printArray(int arr[], int n)
{
    for (int i = 0; i < n; i++)
        System.out.print(arr[i] + " ");
}

// Driver function 
public static void main(String argc[]){
    int arr[] = { 3, 6, 12, 1, 5, 8 };
    int n = 6;

    System.out.print("Original Array: ");
    printArray(arr, n);

    arrangeOddAndEven(arr, n);

    System.out.print("\nModified Array: ");
    printArray(arr, n);
}
}

// This code is contributed by Sagar Shukla 
```

## 蟒蛇 3

```

# Python3 implementation to
# arrange odd and even numbers

def arrangeOddAndEven(arr,  n):

    oddInd = 1
    evenInd = 0
    while (True):

        while (evenInd < n and arr[evenInd] % 2 == 0):
            evenInd += 2

        while (oddInd < n and arr[oddInd] % 2 == 1):
            oddInd += 2

        if (evenInd < n and oddInd < n):
                temp = arr[evenInd]
                arr[evenInd] = arr[oddInd]
                arr[oddInd] = temp;

        else:
            break

# function to print the array
def printArray(arr,  n):
    for i in range(0,n):
        print(arr[i] , "",end="")

# Driver function 
def main():
    arr = [ 3, 6, 12, 1, 5, 8 ]
    n = 6

    print("Original Array: ",end="")
    printArray(arr, n)

    arrangeOddAndEven(arr, n)

    print("\nModified Array: ",end="")
    printArray(arr, n)

if __name__ == '__main__':
    main()
# This code is contributed by 29AjayKumar
```

## C#

```
// C# implementation to
// arrange odd and even numbers
using System;

class GFG {

    // function to arrange
    // odd and even numbers
    public static void arrangeOddAndEven(int[] arr, int n)
    {
     int oddInd = 1;
     int evenInd = 0;
    while (true)
    {
        while (evenInd < n && arr[evenInd] % 2 == 0)
            evenInd += 2;

        while (oddInd < n && arr[oddInd] % 2 == 1)
            oddInd += 2;

        if (evenInd < n && oddInd < n)
            {
                int temp = arr[evenInd];
                arr[evenInd] = arr[oddInd];
                arr[oddInd] = temp;
            }

        else
            break;
    }
    }

    // function to print the array
    public static void printArray(int[] arr, int n)
    {
        for (int i = 0; i < n; i++)
            Console.Write(arr[i] + " ");
    }

    // Driver function
    public static void Main()
    {
        int[] arr = { 3, 6, 12, 1, 5, 8 };
        int n = 6;

        Console.Write("Original Array: ");
        printArray(arr, n);

        arrangeOddAndEven(arr, n);

        Console.Write("\nModified Array: ");
        printArray(arr, n);
    }
}

// This code is contributed by Sam007
```

## java 描述语言

```
<script>

// Javascript implementation to arrange 
// odd and even numbers 

// function to arrange odd and even numbers 
function arrangeOddAndEven(arr, n) 
{ 
    let oddInd = 1; 
    let evenInd = 0; 
    while (true) 
    { 
        while (evenInd < n && arr[evenInd] % 2 == 0) 
            evenInd += 2; 

        while (oddInd < n && arr[oddInd] % 2 == 1) 
            oddInd += 2; 

        if (evenInd < n && oddInd < n)
        {
            let temp;
            temp = arr[evenInd]; 
            arr[evenInd] = arr[oddInd]; 
            arr[oddInd] = temp; 
        }    
        else
            break; 
    } 
} 

// function to print the array 
function printArray(arr, n) 
{ 
    for (let i = 0; i < n; i++) 
        document.write(arr[i] + " "); 
} 

// Driver program to test above
    let arr = [ 3, 6, 12, 1, 5, 8 ]; 
    let n = arr.length; 

    document.write("Original Array: "); 
    printArray(arr, n); 

    arrangeOddAndEven(arr, n); 

    document.write("<br>" + "Modified Array: "); 
    printArray(arr, n); 

// This code is contributed by Mayank Tyagi

</script>
```

**输出:**

```
Original Array: 3 6 12 1 5 8 
Modified Array: 6 3 12 1 8 5 
```

**时间复杂度:** O(n)。
**辅助空间:** O(1)。
本文由 [**阿育什·乔哈里**](https://auth.geeksforgeeks.org/profile.php?user=ayushjauhari14) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。