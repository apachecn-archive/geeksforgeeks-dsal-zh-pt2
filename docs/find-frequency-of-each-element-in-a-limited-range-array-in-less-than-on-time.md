# 在不到 O(n)的时间内找到有限范围数组中每个元素的频率

> 原文:[https://www . geeksforgeeks . org/find-有限范围内每个元素的频率-小于准时数组/](https://www.geeksforgeeks.org/find-frequency-of-each-element-in-a-limited-range-array-in-less-than-on-time/)

给定一个正整数排序数组，计算数组中每个元素出现的次数。假设数组中的所有元素都小于某个常数 m。
这样做无需遍历整个数组。即预期时间复杂度小于 0(n)。

**示例:**

```
Input: arr[] = [1, 1, 1, 2, 3, 3, 5,
               5, 8, 8, 8, 9, 9, 10] 
Output:
Element 1 occurs 3 times
Element 2 occurs 1 times
Element 3 occurs 2 times
Element 5 occurs 2 times
Element 8 occurs 3 times
Element 9 occurs 2 times
Element 10 occurs 1 times

Input: arr[] = [2, 2, 6, 6, 7, 7, 7, 11] 
Output:
Element 2 occurs 2 times
Element 6 occurs 2 times
Element 7 occurs 3 times
Element 11 occurs 1 times
```

**方法 1:** 该方法采用线性搜索技术，不使用辅助空间。

*   **方法:**思路是遍历输入数组，如果当前元素和前一个元素相同，则增加元素的频率，否则重置频率并打印元素及其频率。
*   **算法:**
    *   将频率初始化为 1，索引为 1。
    *   从索引位置遍历数组，检查当前元素是否等于前一个元素。
    *   如果是，增加频率和索引，并重复步骤 2。否则，打印元素及其频率，并重复步骤 2。
    *   最后(角例)，打印最后一个元素及其频率。
*   **实施:**

## C++

```
// C++ program to count number of occurrences of
// each element in the array in O(n) time and O(1) space

#include <iostream>
using namespace std;
void findFrequencies(int ele[], int n)
{
    int freq = 1;
    int idx = 1;
    int element = ele[0];
    while (idx < n) {
        // check if the current element is equal to
        // previous element.
        if (ele[idx - 1] == ele[idx]) {
            freq++;
            idx++;
        }
        else {
            cout << element << " " << freq << endl;
            element = ele[idx];
            idx++;

            // reset the frequency
            freq = 1;
        }
    }

    // print the last element and its frequency
    cout << element << " " << freq;
}

int main()
{
    cout << "---frequencies in a sorted array----" << endl;
    int arr[]
        = { 10, 20, 30, 30, 30, 40, 50, 50, 50, 50, 70 };
    int n = sizeof(arr) / sizeof(arr[0]);
    findFrequencies(arr, n);
}

// This code is contributed by anushkaseehh
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count number of occurrences of
// each element in the array in O(n) time and O(1) space

    function void findFrequencies(ele)
    {
        var freq = 1;
        var idx = 1;
        var element = ele[0];
        while (idx < ele.length) {
            // check if the current element is equal to
            // previous element.
            if (ele[idx - 1] == ele[idx]) {
                freq++;
                idx++;
            }
            else {
                document.write(element + " " + freq+ "<br>");
                element = ele[idx];
                idx++;
                // reset the frequency
                freq = 1;
            }
        }
        // print the last element and its frequency
        document.write(element + " " + freq +"<br>");
    }
    // Driver code

        document.write(
            "---frequencies in a sorted array----"+"<br>");
        findFrequencies(new Array (10, 20, 30, 30, 30, 40,
                                    50, 50, 50, 50, 70 ));

//this code is contributed by shivanisinghss2110
```

## 蟒蛇 3

```
# python program to count number of occurrences of
# each element in the array in O(n) time and O(1) space
def findFrequencies(ele, n):

    freq = 1
    idx = 1
    element = ele[0]
    while (idx < n):

        # check if the current element is equal to
        # previous element.
        if (ele[idx - 1] == ele[idx]):
            freq += 1
            idx += 1

        else:
            print(element , " " ,freq);
            element = ele[idx]
            idx += 1

            # reset the frequency
            freq = 1

    # print the last element and its frequency
    print(element , " " , freq);

print( "---frequencies in a sorted array----" );
arr = [10, 20, 30, 30, 30, 40, 50, 50, 50, 50, 70 ];
n = len(arr)
findFrequencies(arr, n)

# This code is contributed by shivanisinghss2110
```

## C#

```
// C# program to count number of occurrences of
// each element in the array in O(n) time and O(1) space
using System;
class GFG {

    public static void findFrequencies(int[] ele)
    {
        int freq = 1;
        int idx = 1;
        int element = ele[0];
        while (idx < ele.Length)
        {

            // check if the current element is equal to
            // previous element.
            if (ele[idx - 1] == ele[idx]) {
                freq++;
                idx++;
            }
            else {
                Console.WriteLine(element + " " + freq);
                element = ele[idx];
                idx++;

                // reset the frequency
                freq = 1;
            }
        }

        // print the last element and its frequency
        Console.WriteLine(element + " " + freq);
    }

    // Driver code
    public static void Main(String[] args)
    {
        Console.WriteLine(
            "---frequencies in a sorted array----");
        findFrequencies(new int[] { 10, 20, 30, 30, 30, 40,
                                    50, 50, 50, 50, 70 });
    }
}
```

## java 描述语言

```
<script>
// JavaScript program to count number of occurrences of
// each element in the array in O(n) time and O(1) space
    function void findFrequencies(ele)
    {
        var freq = 1;
        var idx = 1;
        var element = ele[0];
        while (idx < ele.length)
        {

            // check if the current element is equal to
            // previous element.
            if (ele[idx - 1] == ele[idx]) {
                freq++;
                idx++;
            }
            else
            {
                document.write(element + " " + freq);
                element = ele[idx];
                idx++;

                // reset the frequency
                freq = 1;
            }
        }

        // print the last element and its frequency
        document.write(element + " " + freq);
    }

    // Driver code
        document.write(
            "---frequencies in a sorted array----");
        findFrequencies(new var[] { 10, 20, 30, 30, 30, 40,
                                    50, 50, 50, 50, 70 });

// This code is contributed by shivanisinghss2110
</script>
```

**Output**

```
---frequencies in a sorted array----
10 1
20 1
30 3
40 1
50 4
70 1
```