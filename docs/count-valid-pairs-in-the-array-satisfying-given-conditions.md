# 计数满足给定条件的数组中的有效对

> 原文:[https://www . geesforgeks . org/count-数组中的有效对-满足给定条件/](https://www.geeksforgeeks.org/count-valid-pairs-in-the-array-satisfying-given-conditions/)

给定一个整数数组 **arr[]** ，任务是计算 **arr** 中有效元素对的数量。一对 **(arr[x]，arr[y])** 如果
被认为无效

*   **arr[x] < arr[y]**
*   **ABS(arr[x]–arr[y])是奇数**

**注:**对 **(arr[x]、arr[y])** 和 **(arr[y]、arr[x])** 在 **x 时是两个不同的对！= y** ， **i** 所有可能值的**arr【I】**值为 **≤ 120** 。
**举例:**

> **输入:** arr[] = {16，17，18}
> **输出:** 2
> 唯一有效的对是(18，16)
> **输入:** arr[] = {16，16}
> **输出:** 2
> 有效的对是(16，16)和(16，16)

**方法:**不处理所有元素，我们可以处理成对的 **(arr[i]，count)** 表示数组中元素 **arr[i]** 的计数。由于只有 **120** 个可能值，我们对每个元素组进行频率计数，这降低了整体复杂性。
对于每一对 **(arr[x]，countX)** 和 **(arr[y]，country)**，如果满足条件，则总有效对为**countrx * country**。
如果 **arr[x] = arr[y]** ，那么我们多算了一些对。在这种情况下，有效的对将是**countA *(countA–1)**，因为没有元素可以与自己配对。
以下是上述办法的实施:

## C++

```
//C++ implementation of the approach
#include<bits/stdc++.h>
using namespace std;

// Function to return total valid pairs
int ValidPairs(int arr[],int n)
{

    // Initialize count of all the elements
    int count[121]={0};

    // frequency count of all the elements
    for(int i=0;i<n;i++)
        count[arr[i]] += 1;

    int ans = 0;
    for(int i=0;i<n;i++)
        for(int j=0;j<n;j++)
        {
            if( arr[i] < arr[j])
                continue;
            if (abs(arr[i] - arr[j]) % 2 == 1)
                continue;

            // Add total valid pairs
            ans += count[arr[i]]* count[arr[j]];
            if (arr[i] == arr[j])

                // Exclude pairs made with a single element
                // i.e. (x, x)
                ans -= count[arr[i]];
        }
    return ans;
}

// Driver Code
int main()
{
int arr[] = {16, 17, 18};
int n= sizeof(arr)/sizeof(int);

// Function call to print required answer
cout<<(ValidPairs(arr,n));
return 0;
}
//contributed by Arnab Kundu
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//Java implementation of the approach

class GFG{
// Function to return total valid pairs
static int ValidPairs(int arr[],int n)
{

    // Initialize count of all the elements
    int[] count=new int[121];

    // frequency count of all the elements
    for(int i=0;i<n;i++)
        count[arr[i]] += 1;

    int ans = 0;
    for(int i=0;i<n;i++)
        for(int j=0;j<n;j++)
        {
            if( arr[i] < arr[j])
                continue;
            if (Math.abs(arr[i] - arr[j]) % 2 == 1)
                continue;

            // Add total valid pairs
            ans += count[arr[i]]* count[arr[j]];
            if (arr[i] == arr[j])

                // Exclude pairs made with a single element
                // i.e. (x, x)
                ans -= count[arr[i]];
        }
    return ans;
}

// Driver Code
public static void main(String[] args)
{
int arr[] = {16, 17, 18};
int n= arr.length;

// Function call to print required answer
System.out.println(ValidPairs(arr,n));
}
}
// This code contributed by mits
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return total valid pairs
def ValidPairs(arr):

    # Initialize count of all the elements
    count = [0] * 121

    # frequency count of all the elements
    for ele in arr:
        count[ele] += 1

    ans = 0
    for eleX, countX in enumerate(count):
        for eleY, countY in enumerate(count):
            if eleX < eleY:
                continue
            if (abs(eleX - eleY) % 2 == 1):
                continue

            # Add total valid pairs
            ans += countX * countY
            if eleX == eleY:

                # Exclude pairs made with a single element
                # i.e. (x, x)
                ans -= countX

    return ans

# Driver Code
arr = [16, 17, 18]

# Function call to print required answer
print(ValidPairs(arr))
```

## C#

```
//C# implementation of the approach
using System;

class GFG{
// Function to return total valid pairs
static int ValidPairs(int[] arr,int n)
{

    // Initialize count of all the elements
    int[] count=new int[121];

    // frequency count of all the elements
    for(int i=0;i<n;i++)
        count[arr[i]] += 1;

    int ans = 0;
    for(int i=0;i<n;i++)
        for(int j=0;j<n;j++)
        {
            if( arr[i] < arr[j])
                continue;
            if (Math.Abs(arr[i] - arr[j]) % 2 == 1)
                continue;

            // Add total valid pairs
            ans += count[arr[i]]* count[arr[j]];
            if (arr[i] == arr[j])

                // Exclude pairs made with a single element
                // i.e. (x, x)
                ans -= count[arr[i]];
        }
    return ans;
}

// Driver Code
public static void Main()
{
int[] arr =new int[]{16, 17, 18};
int n= arr.Length;

// Function call to print required answer
Console.WriteLine(ValidPairs(arr,n));
}
}
// This code contributed by mits
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
//PHP implementation of the approach

// Function to return total valid pairs
function ValidPairs($arr,$n)
{

    // Initialize count of all the elements
    $count=array_fill(0,121,0);

    // frequency count of all the elements
    for($i=0;$i<$n;$i++)
        $count[$arr[$i]] += 1;

    $ans = 0;
    for($i=0;$i<$n;$i++)
        for($j=0;$j<$n;$j++)
        {
            if( $arr[$i] < $arr[$j])
                continue;
            if (abs($arr[$i] - $arr[$j]) % 2 == 1)
                continue;

            // Add total valid pairs
            $ans += $count[$arr[$i]]* $count[$arr[$j]];
            if ($arr[$i] == $arr[$j])

                // Exclude pairs made with a single element
                // i.e. (x, x)
                $ans -= $count[$arr[$i]];
        }
    return $ans;
}

// Driver Code

$arr = array(16, 17, 18);
$n= count($arr);

// Function call to print required answer
echo (ValidPairs($arr,$n));

//This code is contributed by mits
?>
```

## java 描述语言

```
<script>
// javascript implementation of the approach    
// Function to return total valid pairs
    function ValidPairs(arr , n)
    {

        // Initialize count of all the elements
        var count = Array(121).fill(0);

        // frequency count of all the elements
        for (i = 0; i < n; i++)
            count[arr[i]] += 1;

        var ans = 0;
        for (i = 0; i < n; i++)
            for (j = 0; j < n; j++) {
                if (arr[i] < arr[j])
                    continue;
                if (Math.abs(arr[i] - arr[j]) % 2 == 1)
                    continue;

                // Add total valid pairs
                ans += count[arr[i]] * count[arr[j]];
                if (arr[i] == arr[j])

                    // Exclude pairs made with a single element
                    // i.e. (x, x)
                    ans -= count[arr[i]];
            }
        return ans;
    }

    // Driver Code

        var arr = [ 16, 17, 18 ];
        var n = arr.length;

        // Function call to print required answer
        document.write(ValidPairs(arr, n));

// This code is contributed by umadevi9616
</script>
```

**Output:** 

```
1
```