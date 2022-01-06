# 第一个数组中的元素数大于第二个数组中的元素数，每个元素只考虑一次

> 原文:[https://www . geeksforgeeks . org/第一个数组中的元素计数大于第二个数组中的每个元素仅被视为一次/](https://www.geeksforgeeks.org/count-of-elements-in-first-array-greater-than-second-array-with-each-element-considered-only-once/)

给定两个大小为 **N** 的**排序数组**。任务是在第一个数组中找到最大数量的元素，这些元素的**严格大于第二个数组的元素**，这样一个元素只能被考虑一次。
**举例:**

> **输入:** arr1[] = { 20，30，50 }，arr2[] = { 25，40，60 }
> **输出:** 2
> **说明:**
> 数组 arr1 最大 2 个元素 30 (30 > 25)和 50 (50 > 40)大于 arr2。
> **输入:** arr1[] = { 10，15，20，25，30，35 }，arr2[] = { 12，14，26，32，34，40 }
> **输出:** 4
> **解释:**
> 最大 4 个元素 15 (15 > 12)，20 (20 > 14)，30(30>220

**进场:**

1.  逐一比较从**索引 0** 开始的两个数组的元素。
2.  如果 arr1 索引处的元素大于 arr2 索引处的元素，则**将两个数组的**答案和**索引增加 1。******
3.  如果 arr1 索引处的元素小于或等于 arr 2 索引处的元素，则
    T5 增加 arr 1 的索引。
4.  重复以上步骤，直到任何数组的索引到达最后一个元素。
5.  打印答案

以下是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find greater elements
void findMaxElements(
    int arr1[], int arr2[], int n)
{
    // Index counter for arr1
    int cnt1 = 0;
    // Index counter for arr2
    int cnt2 = 0;
    // To store the maximum elements
    int maxelements = 0;

    while (cnt1 < n && cnt2 < n) {

        // If element is greater,
        // update maxelements and counters
        // for both the arrays
        if (arr1[cnt1] > arr2[cnt2]) {
            maxelements++;
            cnt1++;
            cnt2++;
        }
        else {
            cnt1++;
        }
    }

    // Print the maximum elements
    cout << maxelements << endl;
}

int main()
{
    int arr1[] = { 10, 15, 20, 25, 30, 35 };
    int arr2[] = { 12, 14, 26, 32, 34, 40 };

    int n = sizeof(arr1) / sizeof(arr1[0]);

    findMaxElements(arr1, arr2, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
class Main{    

// Function to find greater elements    
static void findmaxelements(int arr1[], int arr2[], int n)        
{
    // Index counter for arr1
    int cnt1 = 0;

    // Index counter for arr1
    int cnt2 = 0;

    // To store the maximum elements
    int maxelements = 0;        

    while(cnt1 < n && cnt2 < n)    
    {

        // If element is greater,
        // update maxelements and counters
        // for both the arrays
        if(arr1[cnt1] > arr2[cnt2])    
        {    
            maxelements++;    
            cnt1++;    
            cnt2++;    
        }    
        else
        {    
            cnt1++;    
        }    
    }    

    // Print the maximum elements
    System.out.println(maxelements);        
}

// Driver Code   
public static void main(String[] args)
{

    int arr1[] = { 10, 15, 20, 25, 30, 35 };        
    int arr2[] = { 12, 14, 26, 32, 34, 40 };

    findmaxelements(arr1, arr2, arr1.length);    
}    
}    

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to find greater elements        
def findmaxelements(arr1, arr2, n):    

    # Index counter for arr1    
    cnt1 = 0

    # Index counter for arr2
    cnt2 = 0

    # To store the maximum elements
    maxelements = 0   

    # If element is greater,
    # update maxelements and counters
    # for both the arrays
    while cnt1 < n and cnt2 < n :

        if arr1[cnt1] > arr2[cnt2] :    
            maxelements += 1       
            cnt1 += 1   
            cnt2 += 1

        else :    
            cnt1 += 1

    # Print the maximum elements
    print(maxelements)

# Driver Code   
arr1 = [ 10, 15, 20, 25, 30, 35 ]    
arr2 = [ 12, 14, 26, 32, 34, 40 ]

findmaxelements(arr1, arr2, len(arr1))

# This code is contributed by divyeshrabadiya07
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to find greater elements    
static void findmaxelements(int[] arr1,
                            int[] arr2, int n)    
{

    // Index counter for arr1
    int cnt1 = 0;

    // Index counter for arr1
    int cnt2 = 0;

    // To store the maximum elements
    int maxelements = 0;        

    while(cnt1 < n && cnt2 < n)
    {

        // If element is greater, update
        // maxelements and counters for
        // both the arrays
        if(arr1[cnt1] > arr2[cnt2])
        {
            maxelements++;
            cnt1++;
            cnt2++;
        }
        else
        {
            cnt1++;
        }
    }

    // Print the maximum elements
    Console.Write(maxelements);
}

// Driver Code
static public void Main(string[] args)
{

    int[] arr1 = { 10, 15, 20, 25, 30, 35 };        
    int[] arr2 = { 12, 14, 26, 32, 34, 40 };

    findmaxelements(arr1, arr2, arr1.Length);
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to find greater elements
function findMaxElements( arr1, arr2, n)
{
    // Index counter for arr1
    var cnt1 = 0;

    // Index counter for arr2
    var cnt2 = 0;

    // To store the maximum elements
    var maxelements = 0;

    while (cnt1 < n && cnt2 < n) {

        // If element is greater,
        // update maxelements and counters
        // for both the arrays
        if (arr1[cnt1] > arr2[cnt2]) {
            maxelements++;
            cnt1++;
            cnt2++;
        }
        else {
            cnt1++;
        }
    }

    // Print the maximum elements
    document.write( maxelements );
}

var arr1 = [10, 15, 20, 25, 30, 35];
var arr2 = [12, 14, 26, 32, 34, 40];
var n = arr1.length;
findMaxElements(arr1, arr2, n);

// This code is contributed by rrrtnx.
</script>
```

**Output:** 

```
4
```

***时间复杂度:** O(N)* ，其中 N 为数组长度。
***空间复杂度:** O(1)*