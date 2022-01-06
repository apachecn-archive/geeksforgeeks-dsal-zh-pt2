# 求数组中最小值的频率

> 原文:[https://www . geesforgeks . org/find-数组中最小值的出现频率/](https://www.geeksforgeeks.org/find-frequency-of-smallest-value-in-an-array/)

给定一个由 **N** 个元素组成的数组**。求数组中最小值出现的频率。
**例:**** 

```
**Input :** N = 5, arr[] = {3, 2, 3, 4, 4} 
**Output :** 1
The smallest element in the array is 2 
and it occurs only once.

**Input :** N = 6, arr[] = {4, 3, 5, 3, 3, 6}
**Output :** 3
The smallest element in the array is 3 
and it occurs 3 times.
```

****简单方法**:一个简单的方法是先[在第一次遍历中找到数组](https://www.geeksforgeeks.org/to-find-smallest-and-second-smallest-element-in-an-array/)中的最小元素。然后再次遍历数组，找到最小元素的出现次数。
**高效方法**:高效方法是在一次遍历中完成。
假设第一个元素是电流最小值，那么电流最小值的频率就是 1。现在让我们遍历数组(1 到 N)，我们遇到两种情况:** 

*   **当前元素小于当前最小值:我们将当前最小值更改为等于当前元素，由于这是我们第一次遇到此元素，因此我们将其频率设为 1。**
*   **当前元素等于当前最小值:我们增加当前最小值的频率。**

**以下是上述方法的实现:** 

## **C++**

```
// C++ program to find the frequency of
// minimum element in the array

#include <bits/stdc++.h>
using namespace std;

// Function to find the frequency of the
// smallest value in the array
int frequencyOfSmallest(int n, int arr[])
{
    int mn = arr[0], freq = 1;

    for (int i = 1; i < n; i++) {

        // If current element is smaller
        // than minimum
        if (arr[i] < mn) {
            mn = arr[i];
            freq = 1;
        }
        // If current element is equal
        // to smallest
        else if (arr[i] == mn)
            freq++;
    }

    return freq;
}

// Driver Code
int main()
{
    int N = 5;
    int arr[] = { 3, 2, 3, 4, 4 };

    cout << frequencyOfSmallest(N, arr);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program to find the frequency of
// minimum element in the array
import java.io.*;

class GFG
{

// Function to find the frequency of the
// smallest value in the array
static int frequencyOfSmallest(int n, int arr[])
{
    int mn = arr[0], freq = 1;

    for (int i = 1; i < n; i++)
    {

        // If current element is smaller
        // than minimum
        if (arr[i] < mn)
        {
            mn = arr[i];
            freq = 1;
        }

        // If current element is equal
        // to smallest
        else if (arr[i] == mn)
            freq++;
    }
    return freq;
}

    // Driver Code
    public static void main (String[] args)
    {
        int N = 5;
        int arr[] = { 3, 2, 3, 4, 4 };
        System.out.println (frequencyOfSmallest(N, arr));
    }
}

// This code is contributed by Tushil.
```

## **蟒蛇 3**

```
# Python 3 program to find the frequency of
# minimum element in the array

# Function to find the frequency of the
# smallest value in the array
def frequencyOfSmallest(n,arr):
    mn = arr[0]
    freq = 1

    for i in range(1,n):
        # If current element is smaller
        # than minimum
        if (arr[i] < mn):
            mn = arr[i]
            freq = 1

        # If current element is equal
        # to smallest
        elif(arr[i] == mn):
            freq += 1

    return freq

# Driver Code
if __name__ == '__main__':
    N = 5
    arr = [3, 2, 3, 4, 4]

    print(frequencyOfSmallest(N, arr))

# This code is contributed by
# Surendra_Gangwar
```

## **C#**

```
// C# program to find the frequency of
// minimum element in the array
using System;

class GFG
{

    // Function to find the frequency of the
    // smallest value in the array
    static int frequencyOfSmallest(int n, int []arr)
    {
        int mn = arr[0], freq = 1;

        for (int i = 1; i < n; i++)
        {

            // If current element is smaller
            // than minimum
            if (arr[i] < mn)
            {
                mn = arr[i];
                freq = 1;
            }

            // If current element is equal
            // to smallest
            else if (arr[i] == mn)
                freq++;
        }
        return freq;
    }

    // Driver Code
    public static void Main()
    {
        int N = 5;
        int []arr = { 3, 2, 3, 4, 4 };

        Console.WriteLine(frequencyOfSmallest(N, arr));
    }
}

// This code is contributed by Ryuga
```

## **服务器端编程语言（Professional Hypertext Preprocessor 的缩写）**

```
<?php
// PHP program to find the frequency of
// minimum element in the array

// Function to find the frequency of the
// smallest value in the array
function frequencyOfSmallest($n, $arr)
{
    $mn = $arr[0];
    $freq = 1;

    for ($i = 1; $i < $n; $i++)
    {

        // If current element is smaller
        // than minimum
        if ($arr[$i] < $mn)
        {
            $mn = $arr[$i];
            $freq = 1;
        }
        // If current element is equal
        // to smallest
        else if ($arr[$i] == $mn)
            $freq++;
    }

    return $freq;
}

// Driver Code
$N = 5;
$arr = array( 3, 2, 3, 4, 4 );

print(frequencyOfSmallest($N, $arr));

// This code is contributed by mits
?>
```

## **java 描述语言**

```
<script>
    // Javascript program to find the frequency of
    // minimum element in the array
    // required answer

    // Function to find the frequency of the
    // smallest value in the array
    function frequencyOfSmallest(n, arr)
    {
        let mn = arr[0], freq = 1;

        for (let i = 1; i < n; i++)
        {

            // If current element is smaller
            // than minimum
            if (arr[i] < mn)
            {
                mn = arr[i];
                freq = 1;
            }

            // If current element is equal
            // to smallest
            else if (arr[i] == mn)
                freq++;
        }
        return freq;
    }

    let N = 5;
    let arr = [ 3, 2, 3, 4, 4 ];

    document.write(frequencyOfSmallest(N, arr));

</script>
```

****Output:** 

```
1
```** 

****时间复杂度:** O(N)**