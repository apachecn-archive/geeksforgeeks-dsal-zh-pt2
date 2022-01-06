# 最小指数 I，使得从指数 I 到给定指数的所有元素相等

> 原文:[https://www . geesforgeks . org/minimum-index-i-so-从 index-I 到给定索引-的所有元素都是相等的/](https://www.geeksforgeeks.org/minimum-index-i-such-that-all-the-elements-from-index-i-to-given-index-are-equal/)

给定整数数组 **arr[]** 和整数 **pos** ，任务是找到最小索引 **i** ，使得从索引 **i** 到索引 **pos** 的所有元素相等。

**示例:**

> **输入:** arr[] = {2，1，1，1，5，2}，pos = 3
> **输出:** 1
> 索引范围【1，3】内的元素都等于 1。
> 
> **输入:** arr[] = {2，1，1，1，5，2}，pos = 5
> T3】输出: 5

**简单方法:**从索引**位置–1**开始，反向遍历数组，对于第一个索引 **i** ，这样 **arr[i]！= arr[pos]** 打印 **i + 1** ，这是所需的索引。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum required index
int minIndex(int arr[], int n, int pos)
{
    int num = arr[pos];

    // Start from arr[pos - 1]
    int i = pos - 1;
    while (i >= 0) {
        if (arr[i] != num)
            break;
        i--;
    }

    // All elements are equal
    // from arr[i + 1] to arr[pos]
    return i + 1;
}

// Driver code
int main()
{
    int arr[] = { 2, 1, 1, 1, 5, 2 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int pos = 4;

      // Function Call
    cout << minIndex(arr, n, pos);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Function to return the minimum required index
    static int minIndex(int arr[], int n, int pos)
    {
        int num = arr[pos];

        // Start from arr[pos - 1]
        int i = pos - 1;
        while (i >= 0) {
            if (arr[i] != num)
                break;
            i--;
        }

        // All elements are equal
        // from arr[i + 1] to arr[pos]
        return i + 1;
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = { 2, 1, 1, 1, 5, 2 };
        int n = arr.length;
        int pos = 4;

          // Function Call
        System.out.println(minIndex(arr, n, pos));
    }
}

// This code is contributed by Code_Mech.
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the minimum
# required index
def minIndex(arr, n, pos):

    num = arr[pos]

    # Start from arr[pos - 1]
    i = pos - 1
    while (i >= 0):
        if (arr[i] != num):
            break
        i -= 1

    # All elements are equal
    # from arr[i + 1] to arr[pos]
    return i + 1

# Driver code
arr = [2, 1, 1, 1, 5, 2 ]
n = len(arr)
pos = 4

# Function Call
print(minIndex(arr, n, pos))

# This code is contributed by 
# Mohit Kumar 29
```

## C#

```
// C# implementation of the approach
using System;
class GFG {

    // Function to return the minimum required index
    static int minIndex(int[] arr, int n, int pos)
    {
        int num = arr[pos];

        // Start from arr[pos - 1]
        int i = pos - 1;
        while (i >= 0) {
            if (arr[i] != num)
                break;
            i--;
        }

        // All elements are equal
        // from arr[i + 1] to arr[pos]
        return i + 1;
    }

    // Driver code
    public static void Main()
    {
        int[] arr = { 2, 1, 1, 1, 5, 2 };
        int n = arr.Length;
        int pos = 4;

          // Function Call
        Console.WriteLine(minIndex(arr, n, pos));
    }
}

// This code is contributed
// by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach 

// Function to return the minimum 
// required index 
function minIndex($arr, $n, $pos) 
{ 
    $num = $arr[$pos]; 

    // Start from arr[pos - 1] 
    $i = $pos - 1; 
    while ($i >= 0) 
    { 
        if ($arr[$i] != $num) 
            break; 
        $i--; 
    } 

    // All elements are equal 
    // from arr[i + 1] to arr[pos] 
    return $i + 1; 
} 

// Driver code 
$arr = array(2, 1, 1, 1, 5, 2 ); 
$n = sizeof($arr); 
$pos = 4; 

echo minIndex($arr, $n, $pos); 

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the minimum required index
function minIndex(arr, n, pos)
{
    var num = arr[pos];

    // Start from arr[pos - 1]
    var i = pos - 1;
    while (i >= 0) {
        if (arr[i] != num)
            break;
        i--;
    }

    // All elements are equal
    // from arr[i + 1] to arr[pos]
    return i + 1;
}

// Driver code
var arr = [ 2, 1, 1, 1, 5, 2 ];
var n = arr.length;
var pos = 4;

// Function Call
document.write(minIndex(arr, n, pos));

// This code is contributed by rrrtnx.
</script>
```

**Output**

```
4
```

**时间复杂度:**O(N)
T3】空间复杂度: O(1)

**有效方法:**

在子阵列[0，位置-1]中进行二分搜索法运算。停止条件将是如果 arr[mid] == arr[pos] && arr[mid-1]！= arr[pos]。向左或向右将分别取决于是否有 arr[mid] == arr[pos]。

**实施:**

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum required index
int minIndex(int arr[], int pos)
{
    int low = 0;
    int high = pos;
    int i = pos;

    while (low < high) {
        int mid = (low + high) / 2;
        if (arr[mid] != arr[pos]) {
            low = mid + 1;
        }
        else {
            high = mid - 1;
            i = mid;
            if (mid > 0 && arr[mid - 1] != arr[pos]) {

                // Short-circuit more comparisons as found
                // the border point
                break;
            }
        }
    }

    // For cases were high = low + 1 and arr[high] will
    // match with
    // arr[pos] but not arr[low] or arr[mid]. In such
    // iteration the if condition will satisfy and loop will
    // break post that low will be updated. Hence i will not
    // point to the correct index.
    return arr[low] == arr[pos] ? low : i;
}

// Driver code
int main()
{
    int arr[] = { 2, 1, 1, 1, 5, 2 };

    cout << minIndex(arr, 2) << endl; // Should be 1
    cout << minIndex(arr, 3) << endl; // Should be 1
    cout << minIndex(arr, 4) << endl; // Should be 4
    return 0;
}

// This code is contributed by
// anshbikram
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach

class GFG {

      // Function to return the minimum required index
    static int minIndex(int arr[], int pos)
    {
        int low = 0;
        int high = pos;
        int i = pos;

        while (low < high) {
            int mid = (low + high) / 2;
            if (arr[mid] != arr[pos]) {
                low = mid + 1;
            }
            else {
                high = mid - 1;
                i = mid;
                if (mid > 0 && arr[mid - 1] != arr[pos]) {

                      // Short-circuit more comparisons as
                    // found the border point
                    break;
                }
            }
        }

        // For cases were high = low + 1 and arr[high] will
        // match with arr[pos] but not arr[low] or arr[mid].
        // In such iteration the if condition will satisfy
        // and loop will break post that low will be
        // updated. Hence i will not point to the correct
        // index.
        return arr[low] == arr[pos] ? low : i;
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = { 2, 1, 1, 1, 5, 2 };

        System.out.println(minIndex(arr, 2)); // Should be 1
        System.out.println(minIndex(arr, 3)); // Should be 1
        System.out.println(minIndex(arr, 4)); // Should be 4
    }
}

// This code is contributed by
// anshbikram
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the minimum
# required index

def minIndex(arr, pos):
    low = 0
    high = pos
    i = pos

    while low < high:
        mid = (low + high)//2
        if arr[mid] != arr[pos]:
            low = mid + 1
        else:
            high = mid - 1
            i = mid
            if mid > 0 and arr[mid-1] != arr[pos]:

                # Short-circuit more comparisons as found the border point
                break

    # For cases were high = low + 1 and arr[high] will match with
    # arr[pos] but not arr[low] or arr[mid]. In such iteration
    # the if condition will satisfy and loop will break post that
    # low will be updated. Hence i will not point to the correct index.
    return low if arr[low] == arr[pos] else i

# Driver code
arr = [2, 1, 1, 1, 5, 2]

print(minIndex(arr, 2))  # Should be 1
print(minIndex(arr, 3))  # Should be 1
print(minIndex(arr, 4))  # Should be 4

# This code is contributed by
# anshbikram
```

## C#

```
// C# implementation of the approach
using System;

class GFG{

// Function to return the minimum 
// required index
static int minIndex(int []arr, int pos)
{
    int low = 0;
    int high = pos;
    int i = pos;

    while (low < high)
    {
        int mid = (low + high) / 2;
        if (arr[mid] != arr[pos]) 
        {
            low = mid + 1;
        }
        else 
        {
            high = mid - 1;
            i = mid;
            if (mid > 0 && arr[mid - 1] != arr[pos]) 
            {

                // Short-circuit more comparisons as
                // found the border point
                break;
            }
        }
    }

    // For cases were high = low + 1 and arr[high] will
    // match with arr[pos] but not arr[low] or arr[mid].
    // In such iteration the if condition will satisfy
    // and loop will break post that low will be
    // updated. Hence i will not point to the correct
    // index.
    return arr[low] == arr[pos] ? low : i;
}

// Driver code
public static void Main()
{
    int []arr = { 2, 1, 1, 1, 5, 2 };

    Console.WriteLine(minIndex(arr, 2)); // Should be 1
    Console.WriteLine(minIndex(arr, 3)); // Should be 1
    Console.WriteLine(minIndex(arr, 4)); // Should be 4
}
}

// This code is contributed by chitranayal
```

## java 描述语言

```
<script>
// javascript implementation of the approach
    // Function to return the minimum required index
    function minIndex(arr , pos) {
        var low = 0;
        var high = pos;
        var i = pos;

        while (low < high) {
            var mid = parseInt((low + high) / 2);
            if (arr[mid] != arr[pos]) {
                low = mid + 1;
            } else {
                high = mid - 1;
                i = mid;
                if (mid > 0 && arr[mid - 1] != arr[pos]) {

                    // Short-circuit more comparisons as
                    // found the border point
                    break;
                }
            }
        }

        // For cases were high = low + 1 and arr[high] will
        // match with arr[pos] but not arr[low] or arr[mid].
        // In such iteration the if condition will satisfy
        // and loop will break post that low will be
        // updated. Hence i will not point to the correct
        // index.
        return arr[low] == arr[pos] ? low : i;
    }

    // Driver code

        var arr = [ 2, 1, 1, 1, 5, 2 ];

        document.write(minIndex(arr, 2)+"<br/>"); // Should be 1
        document.write(minIndex(arr, 3)+"<br/>"); // Should be 1
        document.write(minIndex(arr, 4)+"<br/>"); // Should be 4

// This code is contributed by todaysgaurav 
</script>
```

**Output**

```
1
1
4
```

**时间复杂度:** O(log(n))
**空间复杂度:** O(1)