# 数组中没有更大元素的元素

> 原文:[https://www . geesforgeks . org/elements-no-element-biger-array/](https://www.geeksforgeeks.org/elements-no-element-bigger-array/)

给定一个整数数组，任务是找到元素的个数，在此之前所有的元素都是较小的。第一个元素总是被计算在内，因为它之前没有其他元素。

**示例:**

```
 Input :  arr[] = {10, 40, 23, 35, 50, 7}
 Output : 3
The elements are 10, 40 and 50.

 Input :  arr[] = {5, 4, 1}
 Output : 1 
```

一种**天真的**方法是一个接一个地考虑一个元素，并检查之前的所有元素。如果一个元素大于全部，则递增结果。

一种**高效的**方法是在数组中的每个索引处存储最大值，如果下一个元素大于最大值，则递增结果并用该元素更新最大值。

下面是这个方法的实现。

## C++

```
// C++ program to find elements that are greater than all
// previous elements
#include <bits/stdc++.h>
using namespace std;

// Function to count elements that are greater than all
// previous elements
int countElements(int arr[], int n)
{
    // First element will always be considered as greater
    // than previous ones
    int result = 1;

    // Store the arr[0] as maximum
    int max_ele = arr[0];

    // Traverse array starting from second element
    for (int i = 1; i < n; i++) {
        // Compare current element with the maximum
        // value if it is true otherwise continue
        if (arr[i] > max_ele) {
            // Update the maximum value
            max_ele = arr[i];

            // Increment the result
            result++;
        }
    }

    return result;
}

// Driver code
int main()
{
    int arr[] = { 10, 40, 23, 35, 50, 7 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << countElements(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find elements that are greater than all
// previous elements

class Test {
    // Method to count elements that are greater than all
    // previous elements
    static int countElements(int arr[], int n)
    {
        // First element will always be considered as greater
        // than previous ones
        int result = 1;

        // Store the arr[0] as maximum
        int max_ele = arr[0];

        // Traverse array starting from second element
        for (int i = 1; i < n; i++) {
            // Compare current element with the maximum
            // value if it is true otherwise continue
            if (arr[i] > max_ele) {
                // Update the maximum value
                max_ele = arr[i];

                // Increment the result
                result++;
            }
        }

        return result;
    }

    // Driver method
    public static void main(String[] args)
    {
        int arr[] = { 10, 40, 23, 35, 50, 7 };
        System.out.println(countElements(arr, arr.length));
    }
}
```

## 蟒蛇 3

```
# Python 3 program to find
# elements that are greater
# than all previous elements

# Function to count elements
# that are greater than all
# previous elements
def countElements(arr, n):

    # First element will always
    # be considered as greater
    # than previous ones
    result = 1

    # Store the arr[0]
    # as maximum
    max_ele = arr[0]

    # Traverse array starting
    # from second element
    for i in range(1, n ):
        # Compare current element
        # with the maximum
        # value if it is true
        # otherwise continue
        if (arr[i] > max_ele):

            # Update the
            # maximum value
            max_ele = arr[i]

            # Increment
            # the result
            result += 1

    return result

# Driver code
arr = [10, 40, 23,
       35, 50, 7]
n = len(arr)
print(countElements(arr, n))

# This code is contributed
# by Smitha
```

## C#

```
// C# program to find elements that
// are greater than all previous elements
using System;

class GFG {

    // Method to count elements that are
    // greater than all previous elements
    static int countElements(int[] arr, int n)
    {
        // First element will always be considered
        // as greater than previous ones
        int result = 1;

        // Store the arr[0] as maximum
        int max_ele = arr[0];

        // Traverse array starting from second element
        for (int i = 1; i < n; i++) {

            // Compare current element with the maximum
            // value if it is true otherwise continue
            if (arr[i] > max_ele) {

                // Update the maximum value
                max_ele = arr[i];

                // Increment the result
                result++;
            }
        }

        return result;
    }

    // Driver method
    public static void Main()
    {
        int[] arr = { 10, 40, 23, 35, 50, 7 };
        Console.WriteLine(countElements(arr, arr.Length));
    }
}

// This code is contributed by Sam007
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find elements that
// are greater than all previous
// elements

// Function to count elements that
// are greater than all previous
// elements
function countElements($arr, $n)
{

    // First element will always
    // be considered as greater
    // than previous ones
    $result = 1;

    // Store the arr[0]
    // as maximum
    $max_ele = $arr[0];

    // Traverse array starting
    // from second element
    for($i = 1; $i < $n; $i++)
    {

        // Compare current element
        // with the maximum value
        // if it is true otherwise
        // continue
        if ($arr[$i] > $max_ele)
        {

            // Update the maximum value
            $max_ele = $arr[$i];

            // Increment the result
            $result++;
        }
    }

    return $result;
}

    // Driver code
    $arr = array(10, 40, 23, 35, 50, 7);
    $n = sizeof($arr);
    echo countElements($arr, $n);

// This code is contributed by nitin mittal.
?>
```

## java 描述语言

```
<script>
    // Javascript program to find elements that
    // are greater than all previous elements

    // Method to count elements that are
    // greater than all previous elements
    function countElements(arr, n)
    {
        // First element will always be considered
        // as greater than previous ones
        let result = 1;

        // Store the arr[0] as maximum
        let max_ele = arr[0];

        // Traverse array starting from second element
        for (let i = 1; i < n; i++) {

            // Compare current element with the maximum
            // value if it is true otherwise continue
            if (arr[i] > max_ele) {

                // Update the maximum value
                max_ele = arr[i];

                // Increment the result
                result++;
            }
        }

        return result;
    }

    let arr = [ 10, 40, 23, 35, 50, 7 ];
      document.write(countElements(arr, arr.length));

</script>
```

**输出:**

```
3
```

**时间复杂度:** O(n)，其中 n 是输入中的元素个数。
**辅助空间:** O(1)

本文由 [**萨哈布拉**](https://www.facebook.com/sahil.chhabra.965) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，或者想分享更多关于上述话题的信息，请写评论。