# 在 O(n)个时间和 O(1)个额外空间中查找重复|设置 1

> 原文:[https://www . geesforgeks . org/find-time-in-duplicates-on-constant-extra-space/](https://www.geeksforgeeks.org/find-duplicates-in-on-time-and-constant-extra-space/)

给定包含从 0 到 n-1 的元素的 n 个元素的数组，这些数字中的任何一个出现任意次数。在 O(n)中找到这些重复的数字，并且只使用恒定的内存空间。

**示例:**

```
Input : n = 7 and array[] = {1, 2, 3, 6, 3, 6, 1}
Output: 1, 3, 6

Explanation: The numbers 1 , 3 and 6 appears more
than once in the array.

Input : n = 5 and array[] = {1, 2, 3, 4 ,3}
Output: 3

Explanation: The number 3 appears more than once
in the array.
```

**这个问题是以下问题的扩展版。**
[找到给定数组中的两个重复元素](https://www.geeksforgeeks.org/find-the-two-repeating-elements-in-a-given-array/)
上述环节的方法 1 和方法 2 不适用，因为问题说的是 O(n)时间复杂度和 O(1)常数空间。此外，方法 3 和方法 4 不能在这里应用，因为在这个问题中可以有 2 个以上的重复元素。方法 5 可以扩展到解决这个问题。下面是类似于方法 5 的解决方案。

**<u>解决方案 1:</u>**

*   **逼近:**数组中的元素从 0 到 n-1，全部为正。所以要找出重复的元素，需要一个 HashMap，但问题是要在常数空间中解决这个问题。有一个陷阱，数组长度为 n，元素从 0 到 n-1 (n 个元素)。该数组可以用作哈希映射。
    **问题在下面逼近。**这种方法只适用于最多有 2 个重复元素的数组，也就是说，如果数组包含 2 个以上的重复元素，这种方法将不起作用。例如:{1，6，3，1，3，6，6}它将输出为:1 3 6 6。
*   **注意:**上述程序不处理 0 的情况(如果数组中存在 0)。该程序可以很容易地修改，以处理这一点。保持代码简单并不是一件容易的事。(通过将所有值加 1(+1)，可以修改程序以处理 0 种情况。同样从答案中减去 1，并用代码写下

****在下面的其他方法中，讨论了仅打印重复元素一次的解决方案。**
**算法:**** 

1.  **从头到尾遍历数组。**
2.  **对于每个元素，取其绝对值，如果 *abs(数组[i])* 的第个元素是正的，则该元素以前没有遇到过，否则如果是负的，则该元素在打印当前元素的绝对值之前已经遇到过。**

****实施:****

## **C++**

```
// C++ code to find
// duplicates in O(n) time
#include <bits/stdc++.h>
using namespace std;

// Function to print duplicates
void printRepeating(int arr[], int size)
{
    int i;
    cout << "The repeating elements are:" << endl;
    for (i = 0; i < size; i++) {
        if (arr[abs(arr[i])] >= 0)
            arr[abs(arr[i])] = -arr[abs(arr[i])];
        else
            cout << abs(arr[i]) << " ";
    }
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 3, 1, 3, 6, 6 };
    int arr_size = sizeof(arr) / sizeof(arr[0]);
    printRepeating(arr, arr_size);
    return 0;
}

// This code is contributed
// by Akanksha Rai
```

## **C**

```
// C code to find
// duplicates in O(n) time
#include <stdio.h>
#include <stdlib.h>

// Function to print duplicates
void printRepeating(int arr[], int size)
{
    int i;
    printf("The repeating elements are: \n");
    for (i = 0; i < size; i++) {
        if (arr[abs(arr[i])] >= 0)
            arr[abs(arr[i])] = -arr[abs(arr[i])];
        else
            printf(" %d ", abs(arr[i]));
    }
}

// Driver Code
int main()
{
    int arr[] = { 1, 2, 3, 1, 3, 6, 6 };
    int arr_size = sizeof(arr) / sizeof(arr[0]);
    printRepeating(arr, arr_size);
    getchar();
    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java code to find
// duplicates in O(n) time

class FindDuplicate {
    // Function to print duplicates
    void printRepeating(int arr[], int size)
    {
        int i;
        System.out.println("The repeating elements are : ");

        for (i = 0; i < size; i++) {
            int j = Math.abs(arr[i]);
            if (arr[j] >= 0)
                arr[j] = -arr[j];
            else
                System.out.print(j + " ");
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        FindDuplicate duplicate = new FindDuplicate();
        int arr[] = { 1, 2, 3, 1, 3, 6, 6 };
        int arr_size = arr.length;

        duplicate.printRepeating(arr, arr_size);
    }
}

// This code has been contributed by Mayank Jaiswal
```

## **计算机编程语言**

```
# Python3 code to find
# duplicates in O(n) time

# Function to print duplicates

def printRepeating(arr, size):

    print("The repeating elements are: ")

    for i in range(0, size):

        if arr[abs(arr[i])] >= 0:
            arr[abs(arr[i])] = -arr[abs(arr[i])]
        else:
            print(abs(arr[i]), end=" ")

# Driver code
arr = [1, 2, 3, 1, 3, 6, 6]
arr_size = len(arr)

printRepeating(arr, arr_size)

# This code is contributed by Shreyanshi Arun.
```

## **C#**

```
// C# code to find
// duplicates in O(n) time
using System;

class GFG {
    static void printRepeating(int[] arr, int size)
    {
        int i;

        Console.Write("The repeating" +
                      " elements are : ");

        for (i = 0; i < size; i++) {
            int j = Math.Abs(arr[i]);
            if (arr[j] >= 0)
                arr[j] = -arr[j];
            else
                Console.Write(j + " ");
        }
    }

    // Driver code
    public static void Main()
    {
        int[] arr = { 1, 2, 3, 1, 3, 6, 6 };
        int arr_size = arr.Length;

        printRepeating(arr, arr_size);
    }
}

// This code is contributed by Sam007
```

## **服务器端编程语言（Professional Hypertext Preprocessor 的缩写）**

```
<?php
// PHP program to Find duplicates in O(n)
// time and O(1) extra space | Set 1

function printRepeating($arr, $size)
{

    echo "The repeating elements are: \n";
    for ($i = 0; $i < $size; $i++)
    {
        if ($arr[abs($arr[$i])] >= 0)
            $arr[abs($arr[$i])] = -$arr[abs($arr[$i])];
        else
            echo abs($arr[$i]) . " ";
    }
}

// Driver Code
$arr = array(1, 2, 3, 1, 3, 6, 6);
$arr_size = count($arr);
printRepeating($arr, $arr_size);

// This code is contributed by Sam007
?>
```

## **java 描述语言**

```
<script>
// JavaScript code to find
// duplicates in O(n) time

// Function to print duplicates
function printRepeating(arr, size)
{
    let i;
    document.write("The repeating elements are:" + "<br>");
    for (i = 0; i < size; i++) {
        var abs_value = Math.abs(arr[i]);
        if (arr[abs_value] >= 0)
            arr[abs_value] = -arr[abs_value];
        else
            document.write(abs_value + " ");
    }
}

// Driver Code
    let arr = [ 1, 2, 3, 1, 3, 6, 6 ];
    let arr_size = arr.length;
    printRepeating(arr, arr_size);

// This code is contributed by Surbhi Tyagi.

</script>
```

****输出:****

```
The repeating elements are:
1  3  6
```

****复杂度分析:****

*   ****时间复杂度:** O(n)，只需要一次遍历，所以时间复杂度为 O(n)**
*   ****辅助空间:** O(1)，不需要额外空间，所以空间复杂度不变。**

****<u>备选方案</u> :****

*   ****方法:**基本思路是用一个 HashMap 来解决问题。但是有一个问题，数组中的数字是从 0 到 n-1，输入数组的长度是 n。所以，输入数组可以用作哈希映射。遍历数组时，如果遇到元素“a”，则将第%n 个元素的值增加 n。频率可以通过将第% n 个元素除以 n 来获取**
*   ****算法:**

    1.  从头到尾遍历给定的数组。
    2.  对于数组中的每个元素，将 arr[i]%n 个元素递增 n。
    3.  现在再次遍历数组，打印 arr[I/n]大于 1 的所有索引 I。这保证了数字 n 已经被添加到该索引中
    4.  这种方法之所以有效，是因为所有元素都在 0 到 n-1 的范围内，只有当值“I”出现多次时，arr[i]才会大于 n。** 

****实施:****

## **C++**

```
// C++ code to find
// duplicates in O(n) time
#include <bits/stdc++.h>
using namespace std;

int main()
{

    int numRay[] = { 0, 4, 3, 2, 7, 8, 2, 3, 1 };
    int arr_size = sizeof(numRay) / sizeof(numRay[0]);

    // count the frequency
    for (int i = 0; i < arr_size; i++) {
        numRay[numRay[i] % arr_size]
            = numRay[numRay[i] % arr_size] + arr_size;
    }
    cout << "The repeating elements are : " << endl;
    for (int i = 0; i < arr_size; i++) {
        if (numRay[i] >= arr_size * 2) {
            cout << i << " " << endl;
        }
    }
    return 0;
}

// This code is contributed by PrinciRaj1992
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// JAVA code to find
// duplicates in O(n) time

class Leet442 {

    public static void main(String args[])
    {
        int numRay[] = { 0, 4, 3, 2, 7, 8, 2, 3, 1 };

        for (int i = 0; i < numRay.length; i++) {
            numRay[numRay[i] % numRay.length]
                = numRay[numRay[i] % numRay.length]
                  + numRay.length;
        }
        System.out.println("The repeating elements are : ");
        for (int i = 0; i < numRay.length; i++) {
            if (numRay[i] >= numRay.length * 2) {
                System.out.println(i + " ");
            }
        }
    }
}
```

## **计算机编程语言**

```
# Python3 code to find duplicates in O(n) time
numRay = [0, 4, 3, 2, 7, 8, 2, 3, 1]
arr_size = len(numRay)
for i in range(arr_size):

    x = numRay[i] % arr_size
    numRay[x] = numRay[x] + arr_size

print("The repeating elements are : ")
for i in range(arr_size):
    if (numRay[i] >= arr_size*2):
        print(i, " ")

# This code is contributed by 29AjayKumar
```

## **C#**

```
// C# code to find
// duplicates in O(n) time
using System;
class Leet442
{
    public static void Main(String []args)
    {
        int []numRay = { 0, 4, 3, 2, 7, 8, 2, 3, 1 };

        for (int i = 0; i < numRay.Length; i++)
        {
            numRay[numRay[i] % numRay.Length]
                = numRay[numRay[i] % numRay.Length]
                + numRay.Length;
        }
        Console.WriteLine("The repeating elements are : ");
        for (int i = 0; i < numRay.Length; i++)
        {
            if (numRay[i] >= numRay.Length * 2)
            {
                Console.WriteLine(i + " ");
            }
        }
    }
}

// This code is contributed by shivanisinghss2110
```

## **java 描述语言**

```
<script>
    // Javascript code to find
    // duplicates in O(n) time
    let numRay = [ 0, 4, 3, 2, 7, 8, 2, 3, 1 ];
    let arr_size = numRay.length;

    // count the frequency
    for (let i = 0; i < arr_size; i++) {
        numRay[numRay[i] % arr_size]
            = numRay[numRay[i] % arr_size] + arr_size;
    }
    document.write("The repeating elements are : " + "</br>");
    for (let i = 0; i < arr_size; i++) {
        if (numRay[i] >= arr_size * 2) {
            document.write(i + " " + "</br>");
        }
    }

// This code is contributed by mukesh07.
</script>
```

****输出:****

```
The repeating elements are : 
2 
3
```

****复杂度分析:****

*   ****时间复杂度:** O(n)。
    只需要两次遍历。所以时间复杂度是 O(n)。**
*   ****辅助空间:** O(1)。
    不需要额外的空间，所以空间复杂度不变。**