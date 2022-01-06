# 查找数组中是否有一个元素的值是数组和的一半

> 原文:[https://www . geeksforgeeks . org/find-if-array-有一个元素的值是数组和的一半/](https://www.geeksforgeeks.org/find-if-array-has-an-element-whose-value-is-half-of-array-sum/)

给定一个排序的数组(具有唯一的条目)，我们必须找到是否存在一个元素(比如 X)，它正好是包含 X 的数组所有元素总和的一半

**示例:**

```
Input : A = {1, 2, 3}
Output : YES
Sum of all the elements is 6 = 3*2;

Input : A = {2, 4}
Output : NO
Sum of all the elements is 6, and 3 is not present in the array.
```

1.计算数组中所有元素的总和。
2。可以有两种情况
….a. Sum 为奇数，表示我们找不到这样的 X，因为所有条目都是整数。
….b .和为偶数，如果数组中存在和的一半值，则答案为是，否则为否
3。我们可以使用二分搜索法来查找 sum/2 在数组中是否存在(因为它没有重复的条目)

下面是上述方法的实现:

## C++

```
// CPP program to check if array has an
// element whose value is half of array
// sum.
#include <bits/stdc++.h>
using namespace std;

// Function to check if answer exists
bool checkForElement(int array[], int n)
{
    // Sum of all array elements
    int sum = 0;
    for (int i = 0; i < n; i++)
        sum += array[i];

    // If sum is odd
    if (sum % 2)
       return false;

    sum /= 2; // If sum is Even

    // Do binary search for the required element
    int start = 0;
    int end = n - 1;
    while (start <= end)
    {
        int mid = start + (end - start) / 2;
        if (array[mid] == sum)
            return true;       
        else if (array[mid] > sum)
            end = mid - 1;       
        else
            start = mid + 1;
    }

    return false;
}

// Driver code
int main()
{
    int array[] = { 1, 2, 3 };
    int n = sizeof(array) / sizeof(array[0]);
    if (checkForElement(array, n))
      cout << "Yes";
    else
      cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if array has an
// element whose value is half of array
// sum.

import java.io.*;

class GFG {

// Function to check if answer exists
static boolean checkForElement(int array[], int n)
{
    // Sum of all array elements
    int sum = 0;
    for (int i = 0; i < n; i++)
        sum += array[i];

    // If sum is odd
    if (sum % 2>0)
    return false;

    sum /= 2; // If sum is Even

    // Do binary search for the required element
    int start = 0;
    int end = n - 1;
    while (start <= end)
    {
        int mid = start + (end - start) / 2;
        if (array[mid] == sum)
            return true;    
        else if (array[mid] > sum)
            end = mid - 1;    
        else
            start = mid + 1;
    }

    return false;
}

// Driver code

    public static void main (String[] args) {
    int array[] = { 1, 2, 3 };
    int n = array.length;
    if (checkForElement(array, n))
    System.out.println( "Yes");
    else
    System.out.println( "No");
    }
}
// This code is contributed by anuj_67..
```

## 蟒蛇 3

```
# Python 3 program to check if array
# has an element whose value is half
# of array sum.

# Function to check if answer exists
def checkForElement(array, n):

    # Sum of all array elements
    sum = 0
    for i in range(n):
        sum += array[i]

    # If sum is odd
    if (sum % 2):
        return False

    sum //= 2     # If sum is Even

    # Do binary search for the
    # required element
    start = 0
    end = n - 1
    while (start <= end) :
        mid = start + (end - start) // 2
        if (array[mid] == sum):
            return True   
        elif (array[mid] > sum) :
            end = mid - 1;    
        else:
            start = mid + 1

    return False

# Driver code
if __name__ == "__main__":
    array = [ 1, 2, 3 ]
    n = len(array)
    if (checkForElement(array, n)):
        print("Yes")
    else:
        print("No")

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# program to check if array has
// an element whose value is half
// of array sum.
using System;

class GFG
{
// Function to check if answer exists
static bool checkForElement(int[] array,
                            int n)
{
    // Sum of all array elements
    int sum = 0;
    for (int i = 0; i < n; i++)
        sum += array[i];

    // If sum is odd
    if (sum % 2 > 0)
    return false;

    sum /= 2; // If sum is Even

    // Do binary search for the
    // required element
    int start = 0;
    int end = n - 1;
    while (start <= end)
    {
        int mid = start + (end - start) / 2;
        if (array[mid] == sum)
            return true;    
        else if (array[mid] > sum)
            end = mid - 1;    
        else
            start = mid + 1;
    }

    return false;
}

// Driver Code
static void Main()
{
    int []array = { 1, 2, 3 };
    int n = array.Length;
    if (checkForElement(array, n))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}
}

// This code is contributed by ANKITRAI1
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if array has an
// element whose value is half of array
// sum.

// Function to check if answer exists
function checkForElement(&$array, $n)
{
    // Sum of all array elements
    $sum = 0;
    for ($i = 0; $i < $n; $i++)
        $sum += $array[$i];

    // If sum is odd
    if ($sum % 2)
    return false;

    $sum /= 2; // If sum is Even

    // Do binary search for the
    // required element
    $start = 0;
    $end = $n - 1;
    while ($start <= $end)
    {
        $mid = $start + ($end - $start) / 2;
        if ($array[$mid] == $sum)
            return true;    
        else if ($array[$mid] > $sum)
            $end = $mid - 1;    
        else
            $start = $mid + 1;
    }

    return false;
}

// Driver code
$array = array(1, 2, 3 );
$n = sizeof($array);
if (checkForElement($array, $n))
    echo "Yes";
else
    echo "No";

// This code is contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>
// Javascript program to check if array has an
// element whose value is half of array
// sum.

// Function to check if answer exists
function checkForElement(array, n)
{

    // Sum of all array elements
    let sum = 0;
    for (let i = 0; i < n; i++)
        sum += array[i];

    // If sum is odd
    if (sum % 2)
    return false;

    sum = Math.floor(sum / 2); // If sum is Even

    // Do binary search for the
    // required element
    let start = 0;
    let end = n - 1;
    while (start <= end)
    {
        let mid = Math.floor(start + (end - start) / 2);
        if (array[mid] == sum)
            return true;    
        else if (array[mid] > sum)
            end = mid - 1;    
        else
            start = mid + 1;
    }

    return false;
}

// Driver code
let array = new Array(1, 2, 3 );
let n = array.length;
if (checkForElement(array, n))
    document.write("Yes");
else
    document.write("No");

// This code is contributed by _saurabh_jaiswal
</script>
```

**Output:** 

```
Yes
```

**时间复杂度:**O(n)
T3】辅助空间: O(1)

**另一个适用于未排序数组的有效解决方案也是**
这个想法是使用哈希。

## C++

```
// CPP program to check if array has an
// element whose value is half of array
// sum.
#include <bits/stdc++.h>
using namespace std;

// Function to check if answer exists
bool checkForElement(int array[], int n)
{
    // Sum of all array elements
    // and storing in a hash table
    unordered_set<int> s;
    int sum = 0;
    for (int i = 0; i < n; i++) {
        sum += array[i];
        s.insert(array[i]);
    }

    // If sum/2 is present in hash table
    if (sum % 2 == 0 && s.find(sum/2) != s.end())
        return true;
    else
        return false;
}

// Driver code
int main()
{
    int array[] = { 1, 2, 3 };
    int n = sizeof(array) / sizeof(array[0]);
    if (checkForElement(array, n))
      cout << "Yes";
    else
      cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if array has an
// element whose value is half of array
// sum.

import java.util.*;

class GFG {

// Function to check if answer exists
    static boolean checkForElement(int array[], int n) {
        // Sum of all array elements
        // and storing in a hash table
        Set<Integer> s = new LinkedHashSet<>();
        int sum = 0;
        for (int i = 0; i < n; i++) {
            sum += array[i];
            s.add(array[i]);
        }
        // If sum/2 is present in hash table
        if (sum % 2 == 0 && s.contains(sum / 2)
                && (sum / 2 )== s.stream().skip(s.size() - 1).findFirst().get()) {
            return true;
        } else {
            return false;
        }
    }

// Driver code
    public static void main(String[] args) {
        int array[] = {1, 2, 3};
        int n = array.length;
        System.out.println(checkForElement(array, n) ? "Yes" : "No");
    }
}
// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python 3 program to check if array has an
# element whose value is half of array
# sum.

# Function to check if answer exists
def checkForElement(array, n):
    # Sum of all array elements
    # and storing in a hash table
    s = set()
    sum = 0
    for i in range(n):
        sum += array[i]
        s.add(array[i])

    # If sum/2 is present in hash table
    f = int(sum / 2)
    if (sum % 2 == 0 and  f in s):
        return True
    else:
        return False

# Driver code
if __name__ == '__main__':
    array = [1, 2, 3]
    n = len(array)
    if (checkForElement(array, n)):
        print("Yes")
    else:
        print("No")

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to check if array has an
// element whose value is half of array
// sum.
using System;
using System.Collections.Generic;

class GFG
{

    // Function to check if answer exists
    static Boolean checkForElement(int []array, int n)
    {
        // Sum of all array elements
        // and storing in a hash table
        HashSet<int> s = new HashSet<int>();
        int sum = 0;
        for (int i = 0; i < n; i++)
        {
            sum += array[i];
            s.Add(array[i]);
        }

        // If sum/2 is present in hash table
        if (sum % 2 == 0 && s.Contains(sum / 2))
        {
            return true;
        }
        else
        {
            return false;
        }
    }

    // Driver code
    public static void Main(String[] args)
    {
        int []array = {1, 2, 3};
        int n = array.Length;
        Console.WriteLine(checkForElement(array, n) ? "Yes" : "No");
    }
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript program to check if array has an
// element whose value is half of array
// sum.

// Function to check if answer exists
function checkForElement(array, n)
{

    // Sum of all array elements
    // and storing in a hash table
    let s = new Set();
    let sum = 0;

    for(let i = 0; i < n; i++)
    {
        sum += array[i];
        s.add(array[i]);
    }

    // If sum/2 is present in hash table
    if (sum % 2 == 0 && s.has(sum / 2))
    {
        return true;
    }
    else
    {
        return false;
    }
}

// Driver code
let array = [ 1, 2, 3 ];
let n = array.length;

document.write(
    checkForElement(array, n) ? "Yes" : "No");

// This code is contributed by rag2127

</script>
```

**Output:** 

```
Yes
```

**时间复杂度:**O(n)
T3】辅助空间: O(n)