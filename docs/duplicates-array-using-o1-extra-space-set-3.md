# 使用 O(1)个额外空间在数组中查找重复项

> 原文:[https://www . geesforgeks . org/duplicates-array-use-O1-extra-space-set-3/](https://www.geeksforgeeks.org/duplicates-array-using-o1-extra-space-set-3/)

给定一个包含 n + 1 个整数的数组 arr[]，其中每个整数都在 1 和 n(包括 1 和 n)之间。只有一个重复元素，在 O(n)时间复杂度和 O(1)空间找到重复元素。
**例:**

```
Input  : arr[] = {1, 4, 3, 4, 2} 
Output : 4

Input  : arr[] = {1, 3, 2, 1}
Output : 1
```

**方法:**
首先，这个问题的约束意味着一个循环必须存在。因为数组 arr[]中的每个数字都在 1 和 n 之间，所以它必然指向一个存在的索引。因此，列表可以无限遍历，这意味着有一个循环。此外，因为 0 不能作为值出现在数组 arr[]中，所以 arr[0]不能是循环的一部分。因此，以这种方式从 arr[0]遍历数组相当于遍历循环链表。这个问题就像[链表循环](https://www.geeksforgeeks.org/detect-loop-in-a-linked-list/)一样可以解决。
以下是上述方法的实施:

## C++

```
// CPP code to find the repeated elements
// in the array where every other is present once
#include <iostream>
using namespace std;

// Function to find duplicate
int findDuplicate(int arr[])
{
    // Find the intersection point of
    // the slow and fast.
    int slow = arr[0];
    int fast = arr[0];
    do
    {
        slow = arr[slow];
        fast = arr[arr[fast]];
    } while (slow != fast);

    // Find the "entrance" to the cycle.
    int ptr1 = arr[0];
    int ptr2 = slow;
    while (ptr1 != ptr2)
    {
        ptr1 = arr[ptr1];
        ptr2 = arr[ptr2];
    }

    return ptr1;
}

// Driver code
int main()
{
    int arr[] = { 1, 3, 2, 1 };

    cout << findDuplicate(arr) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code to find the repeated
// elements in the array where
// every other is present once
import java.util.*;

class GFG
{

// Function to find duplicate
public static int findDuplicate(int []arr)
{
    // Find the intersection
    // point of the slow and fast.
    int slow = arr[0];
    int fast = arr[0];
    do
    {
        slow = arr[slow];
        fast = arr[arr[fast]];
    } while (slow != fast);

    // Find the "entrance"
    // to the cycle.
    int ptr1 = arr[0];
    int ptr2 = slow;
    while (ptr1 != ptr2)
    {
        ptr1 = arr[ptr1];
        ptr2 = arr[ptr2];
    }

    return ptr1;
}

// Driver Code
public static void main(String[] args)
{
    int []arr = {1, 3, 2, 1};

    System.out.println("" +
               findDuplicate(arr));

    System.exit(0);
}
}

// This code is contributed
// by Harshit Saini
```

## 蟒蛇 3

```
# Python code to find the
# repeated elements in the
# array where every other
# is present once

# Function to find duplicate
def findDuplicate(arr):

    # Find the intersection
    # point of the slow and fast.
    slow = arr[0]
    fast = arr[0]
    while True:
        slow = arr[slow]
        fast = arr[arr[fast]]
        if slow == fast:
            break

    # Find the "entrance"
    # to the cycle.
    ptr1 = arr[0]
    ptr2 = slow
    while ptr1 != ptr2:
        ptr1 = arr[ptr1]
        ptr2 = arr[ptr2]

    return ptr1

# Driver code
if __name__ == '__main__':

    arr = [ 1, 3, 2, 1 ]

    print(findDuplicate(arr))

# This code is contributed
# by Harshit Saini
```

## C#

```
// C# code to find the repeated
// elements in the array where
// every other is present once
using System;

class GFG
{

// Function to find duplicate
public static int findDuplicate(int []arr)
{
    // Find the intersection
    // point of the slow and fast.
    int slow = arr[0];
    int fast = arr[0];
    do
    {
        slow = arr[slow];
        fast = arr[arr[fast]];
    } while (slow != fast);

    // Find the "entrance"
    // to the cycle.
    int ptr1 = arr[0];
    int ptr2 = slow;
    while (ptr1 != ptr2)
    {
        ptr1 = arr[ptr1];
        ptr2 = arr[ptr2];
    }

    return ptr1;
}

// Driver Code
public static void Main()
{
    int[] arr = {1, 3, 2, 1};

    Console.WriteLine("" +
            findDuplicate(arr));

}
}

// This code is contributed
// by Akanksha Rai(Abby_akku)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP code to find the repeated
// elements in the array where
// every other is present once

// Function to find duplicate
function findDuplicate(&$arr)
{
    $slow = $arr[0];
    $fast = $arr[0];
    do
    {
        $slow = $arr[$slow];
        $fast = $arr[$arr[$fast]];
    } while ($slow != $fast);

    // Find the "entrance"
    // to the cycle.
    $ptr1 = $arr[0];
    $ptr2 = $slow;
    while ($ptr1 != $ptr2)
    {
        $ptr1 = $arr[$ptr1];
        $ptr2 = $arr[$ptr2];
    }

    return $ptr1;
}

// Driver code
$arr = array(1, 3, 2, 1);
echo " " . findDuplicate($arr);

// This code is contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>
// JavaScript code to find the repeated elements
// in the array where every other is present once

// Function to find duplicate
function findDuplicate(arr)
{

    // Find the intersection point of
    // the slow and fast.
    let slow = arr[0];
    let fast = arr[0];
    do
    {
        slow = arr[slow];
        fast = arr[arr[fast]];
    } while (slow != fast);

    // Find the "entrance" to the cycle.
    let ptr1 = arr[0];
    let ptr2 = slow;
    while (ptr1 != ptr2)
    {
        ptr1 = arr[ptr1];
        ptr2 = arr[ptr2];
    }
    return ptr1;
}

// Driver code
    let arr = [ 1, 3, 2, 1 ];
    document.write(findDuplicate(arr) + "<br>");

// This code is contributed by Surbhi Tyagi.
</script>
```

**Output:** 

```
1
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)