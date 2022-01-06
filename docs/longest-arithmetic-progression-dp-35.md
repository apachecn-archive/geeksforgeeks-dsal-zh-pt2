# 最长算术级数| DP-35

> 原文:[https://www . geesforgeks . org/long-算术级数-dp-35/](https://www.geeksforgeeks.org/longest-arithmetic-progression-dp-35/)

给定一组数字，找出其中 **L** 最长 **A** 算术 **P** 表达式( **LLAP** )的 **L** 长度。

**示例:**

```
set[] = {1, 7, 10, 15, 27, 29}
output = 3
The longest arithmetic progression is {1, 15, 29}

set[] = {5, 10, 15, 20, 25, 30}
output = 6
The whole set is in AP
```

为了简单起见，我们假设给定的集合已经排序。我们总是可以添加一个预处理步骤，首先对集合进行排序，然后应用下面的算法。

一个**简单的解决方案**是一个接一个地将每一对视为 AP 的前两个元素，并检查排序集中的剩余元素。要将所有对视为前两个元素，我们需要运行一个 O(n^2)嵌套循环。在嵌套循环中，我们需要第三个循环，它线性地寻找更多的元素在 **A** 算法 **P** 表达式( **AP** )中。这个过程需要 O(n <sup>3</sup> )时间。
我们可以使用动态编程在 O(n <sup>2</sup> )时间**内解决这个问题。为了了解动力定位解决方案，让我们先来讨论下一个简单问题的解决方案。**

***给定一个排序后的集合，查找算术级数中是否存在三个元素***
请注意，AP 中有 3 个或 3 个以上的元素，则答案为真，否则为假。
要找到这三个元素，我们先固定一个元素作为中间元素，搜索另外两个(一个小一个大)。我们从第二个元素开始，将每个元素固定为中间元素。要使元素集[j]位于 AP 的中间，必须存在元素“集[i]”和“集[k]”，使得集[i] +集[k]= 2 *集[j]，其中 0 < = i < j 和 j < k < =n-1。
*如何高效地找到给定 j 的 I 和 k？*我们可以使用以下简单算法在线性时间内找到 I 和 k。

1.  将 I 初始化为 j-1，将 k 初始化为 j+1
2.  当 i >= 0 且 k <= n-1 时，执行以下操作
    *   如果集合[i] +集合[k]等于 2 *集合[j]，那么我们就完了。
    *   如果 set[i] + set[k] > 2*set[j]，则递减 I(do I–)。
    *   否则如果设置[i] +设置[k]< 2 *设置[j]，则增加 k(做 k++)。

下面是针对更简单问题的上述算法的实现。

## C++

```
// The function returns true if there exist three
// elements in AP Assumption: set[0..n-1] is sorted.
// The code strictly implements the algorithm provided
// in the reference.
bool arithmeticThree(vector<int> set, int n)
{

    // One by fix every element as middle element
    for(int j = 1; j < n - 1; j++)
    {

        // Initialize i and k for the current j
        int i = j - 1, k = j + 1;

        // Find if there exist i and k that form AP
        // with j as middle element
        while (i >= 0 && k <= n-1)
        {
            if (set[i] + set[k] == 2 * set[j])
                return true;

            (set[i] + set[k] < 2 * set[j]) ? k++ : i--;
        }
    }
    return false;
}

// This code is contributed by Samim Hossain Mondal.
```

## C

```
// The function returns true if there exist three elements in AP
// Assumption: set[0..n-1] is sorted.
// The code strictly implements the algorithm provided in the reference.
bool arithmeticThree(int set[], int n)
{
    // One by fix every element as middle element
    for (int j=1; j<n-1; j++)
    {
        // Initialize i and k for the current j
        int i = j-1, k = j+1;

        // Find if there exist i and k that form AP
        // with j as middle element
        while (i >= 0 && k <= n-1)
        {
            if (set[i] + set[k] == 2*set[j])
                return true;
            (set[i] + set[k] < 2*set[j])? k++ : i--;
        }
    }

    return false;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// The function returns true if there exist three elements in AP
// Assumption: set[0..n-1] is sorted.
// The code strictly implements the algorithm provided in the reference.
static boolean arithmeticThree(int set[], int n)
{
    // One by fix every element as middle element
    for (int j = 1; j < n - 1; j++)
    {
        // Initialize i and k for the current j
        int i = j - 1, k = j + 1;

        // Find if there exist i and k that form AP
        // with j as middle element
        while (i >= 0 && k <= n-1)
        {
            if (set[i] + set[k] == 2*set[j])
                return true;
            (set[i] + set[k] < 2*set[j])? k++ : i--;
        }
    }

    return false;
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# The function returns true if there exist three elements in AP
# Assumption: set[0..n-1] is sorted.
# The code strictly implements the algorithm provided in the reference.
def arithematicThree(set_,n):

    # One by fix every element as middle element
    for j in range(n):

        # Initialize i and k for the current j
        i,k=j-1,j+1

        # Find if there exist i and k that form AP
        # with j as middle element
        while i>-1 and k<n:
            if set_[i]+set_[k] == 2*set_[j]:
                return True

            elif set_[i]+set_[k]<2*set_[j]:
                i-=1

            else:
                k+=1
    return False
  # This code is contributed by Kushagra Bansal
```

## C#

```
// The function returns true if there exist three elements in AP
// Assumption: set[0..n-1] is sorted.
// The code strictly implements the algorithm provided in the reference.
static bool arithmeticThree(int []set, int n)
{

    // One by fix every element as middle element
    for (int j = 1; j < n - 1; j++)
    {

        // Initialize i and k for the current j
        int i = j - 1, k = j + 1;

        // Find if there exist i and k that form AP
        // with j as middle element
        while (i >= 0 && k <= n-1)
        {
            if (set[i] + set[k] == 2*set[j])
                return true;
            if(set[i] + set[k] < 2*set[j])
                k++;
            else
                i--;
        }
    }

    return false;
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>
// The function returns true if there exist three elements in AP
// Assumption: set[0..n-1] is sorted.
// The code strictly implements the algorithm provided in the reference.
function arithmeticThree(set, n){
    // One by fix every element as middle element
    for (let j=1; j<n-1; j++)
    {
        // Initialize i and k for the current j
        let i = j-1, k = j+1;

        // Find if there exist i and k that form AP
        // with j as middle element
        while (i >= 0 && k <= n-1)
        {
            if (set[i] + set[k] == 2*set[j])
                return true;
            (set[i] + set[k] < 2*set[j])? k++ : i--;
        }
    }

    return false;
}
</script>
```

完整的运行程序见[本](http://ideone.com/yL6r76)。

***如何针对原问题扩展上述解决方案？***
上述函数返回一个布尔值。原问题所需输出为 **L** 最长 **A** 算法 **P** 表达式( **LLAP** )的 **L** 长度，为整数值。如果给定的集合有两个或更多的元素，那么 LLAP 的值至少是 2(为什么？).
想法是创建一个 2D 表 L[n][n]。该表中的一个条目 L[i][j]存储 LLAP，集合[i]和集合[j]作为 AP 和 j 的前两个元素> i .表的最后一列总是 2(为什么–参见 L[i][j]的含义)。表格的其余部分从右下方到左上方填充。为了填充表格的其余部分，首先固定 j(AP 中的第二个元素)。在 I 和 k 中搜索一个固定的 j，如果 I 和 k 被发现使得 I，j，k 形成一个 AP，那么 L[i][j]的值被设置为 L[j][k] + 1。请注意，当循环从右列遍历到左列时，L[j][k]的值必须已经被填充。

下面是动态规划算法的实现。

## C++

```
// C++ program to find Length of the Longest AP (llap) in a given sorted set.
// The code strictly implements the algorithm provided in the reference.
#include <iostream>
using namespace std;

// Returns length of the longest AP subset in a given set
int lenghtOfLongestAP(int set[], int n)
{
    if (n <= 2)  return n;

    // Create a table and initialize all values as 2\. The value of
    // L[i][j] stores LLAP with set[i] and set[j] as first two
    // elements of AP. Only valid entries are the entries where j>i
    int L[n][n];
    int llap = 2;  // Initialize the result

    // Fill entries in last column as 2\. There will always be
    // two elements in AP with last number of set as second
    // element in AP
    for (int i = 0; i < n; i++)
        L[i][n-1] = 2;

    // Consider every element as second element of AP
    for (int j=n-2; j>=1; j--)
    {
        // Search for i and k for j
        int i = j-1, k = j+1;
        while (i >= 0 && k <= n-1)
        {
           if (set[i] + set[k] < 2*set[j])
               k++;

           // Before changing i, set L[i][j] as 2
           else if (set[i] + set[k] > 2*set[j])
           {   L[i][j] = 2, i--;   }

           else
           {
               // Found i and k for j, LLAP with i and j as first two
               // elements is equal to LLAP with j and k as first two
               // elements plus 1\. L[j][k] must have been filled
               // before as we run the loop from right side
               L[i][j] = L[j][k] + 1;

               // Update overall LLAP, if needed
               llap = max(llap, L[i][j]);

               // Change i and k to fill more L[i][j] values for
               // current j
               i--; k++;
           }
        }

        // If the loop was stopped due to k becoming more than
        // n-1, set the remaining entities in column j as 2
        while (i >= 0)
        {
            L[i][j] = 2;
            i--;
        }
    }
    return llap;
}

/* Driver program to test above function*/
int main()
{
    int set1[] = {1, 7, 10, 13, 14, 19};
    int n1 = sizeof(set1)/sizeof(set1[0]);
    cout <<   lenghtOfLongestAP(set1, n1) << endl;

    int set2[] = {1, 7, 10, 15, 27, 29};
    int n2 = sizeof(set2)/sizeof(set2[0]);
    cout <<   lenghtOfLongestAP(set2, n2) << endl;

    int set3[] = {2, 4, 6, 8, 10};
    int n3 = sizeof(set3)/sizeof(set3[0]);
    cout <<   lenghtOfLongestAP(set3, n3) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find Length of the
// Longest AP (llap) in a given sorted set.
// The code strictly implements the
// algorithm provided in the reference.
import java.io.*;

class GFG
{
    // Returns length of the longest
    // AP subset in a given set
    static int lenghtOfLongestAP(int set[], int n)
    {
        if (n <= 2) return n;

        // Create a table and initialize all
        // values as 2\. The value ofL[i][j] stores
        // LLAP with set[i] and set[j] as first two
        // elements of AP. Only valid entries are
        // the entries where j>i
        int L[][] = new int[n][n];

         // Initialize the result
        int llap = 2;

        // Fill entries in last column as 2.
        // There will always be two elements in
        // AP with last number of set as second
        // element in AP
        for (int i = 0; i < n; i++)
            L[i][n - 1] = 2;

        // Consider every element as second element of AP
        for (int j = n - 2; j >= 1; j--)
        {
            // Search for i and k for j
            int i = j -1 , k = j + 1;
            while (i >= 0 && k <= n - 1)
            {
            if (set[i] + set[k] < 2 * set[j])
                k++;

            // Before changing i, set L[i][j] as 2
            else if (set[i] + set[k] > 2 * set[j])
            {
                L[i][j] = 2; i--;

            }

            else
            {
                // Found i and k for j, LLAP with i and j as first two
                // elements is equal to LLAP with j and k as first two
                // elements plus 1\. L[j][k] must have been filled
                // before as we run the loop from right side
                L[i][j] = L[j][k] + 1;

                // Update overall LLAP, if needed
                llap = Math.max(llap, L[i][j]);

                // Change i and k to fill
                // more L[i][j] values for current j
                i--; k++;
            }
            }

            // If the loop was stopped due
            // to k becoming more than
            // n-1, set the remaining
            // entities in column j as 2
            while (i >= 0)
            {
                L[i][j] = 2;
                i--;
            }
        }
        return llap;
    }

    // Driver program
    public static void main (String[] args)
    {
        int set1[] = {1, 7, 10, 13, 14, 19};
        int n1 = set1.length;
        System.out.println ( lenghtOfLongestAP(set1, n1));

        int set2[] = {1, 7, 10, 15, 27, 29};
        int n2 = set2.length;
        System.out.println(lenghtOfLongestAP(set2, n2));

        int set3[] = {2, 4, 6, 8, 10};
        int n3 = set3.length;
        System.out.println(lenghtOfLongestAP(set3, n3)) ;

    }
}

// This code is contributed by vt_m
```

## 蟒蛇 3

```
# Python 3 program to find Length of the
# Longest AP (llap) in a given sorted set.
# The code strictly implements the algorithm
# provided in the reference

# Returns length of the longest AP
# subset in a given set
def lenghtOfLongestAP(set, n):

    if (n <= 2):
        return n

    # Create a table and initialize all
    # values as 2\. The value of L[i][j]
    # stores LLAP with set[i] and set[j]
    # as first two elements of AP. Only
    # valid entries are the entries where j>i
    L = [[0 for x in range(n)]
            for y in range(n)]
    llap = 2 # Initialize the result

    # Fill entries in last column as 2.
    # There will always be two elements
    # in AP with last number of set as
    # second element in AP
    for i in range(n):
        L[i][n - 1] = 2

    # Consider every element as second
    # element of AP
    for j in range(n - 2, 0, -1):

        # Search for i and k for j
        i = j - 1
        k = j + 1
        while(i >= 0 and k <= n - 1):

            if (set[i] + set[k] < 2 * set[j]):
                k += 1

            # Before changing i, set L[i][j] as 2
            elif (set[i] + set[k] > 2 * set[j]):
                L[i][j] = 2
                i -= 1

            else:

                # Found i and k for j, LLAP with i and j
                # as first two elements are equal to LLAP
                # with j and k as first two elements plus 1.
                # L[j][k] must have been filled before as
                # we run the loop from right side
                L[i][j] = L[j][k] + 1

                # Update overall LLAP, if needed
                llap = max(llap, L[i][j])

                # Change i and k to fill more L[i][j]
                # values for current j
                i -= 1
                k += 1

                # If the loop was stopped due to k
                # becoming more than n-1, set the
                # remaining entities in column j as 2
                while (i >= 0):
                    L[i][j] = 2
                    i -= 1
    return llap

# Driver Code
if __name__ == "__main__":

    set1 = [1, 7, 10, 13, 14, 19]
    n1 = len(set1)
    print(lenghtOfLongestAP(set1, n1))

    set2 = [1, 7, 10, 15, 27, 29]
    n2 = len(set2)
    print(lenghtOfLongestAP(set2, n2))

    set3 = [2, 4, 6, 8, 10]
    n3 = len(set3)
    print(lenghtOfLongestAP(set3, n3))

# This code is contributed by ita_c
```

## C#

```
// C# program to find Length of the
// Longest AP (llap) in a given sorted set.
// The code strictly implements the
// algorithm provided in the reference.
using System;

class GFG
{
// Returns length of the longest
// AP subset in a given set
static int lenghtOfLongestAP(int []set,
                             int n)
{
    if (n <= 2) return n;

    // Create a table and initialize
    // all values as 2\. The value of
    // L[i][j] stores LLAP with set[i] 
    // and set[j] as first two elements
    // of AP. Only valid entries are
    // the entries where j>i
    int [,]L = new int[n, n];

    // Initialize the result
    int llap = 2;

    // Fill entries in last column as 2.
    // There will always be two elements
    // in AP with last number of set as
    // second element in AP
    for (int i = 0; i < n; i++)
        L[i, n - 1] = 2;

    // Consider every element as
    // second element of AP
    for (int j = n - 2; j >= 1; j--)
    {
        // Search for i and k for j
        int i = j - 1 , k = j + 1;
        while (i >= 0 && k <= n - 1)
        {
        if (set[i] + set[k] < 2 * set[j])
            k++;

        // Before changing i, set L[i][j] as 2
        else if (set[i] + set[k] > 2 * set[j])
        {
            L[i, j] = 2; i--;

        }

        else
        {
            // Found i and k for j, LLAP with
            // i and j as first two elements
            // is equal to LLAP with j and k
            // as first two elements plus 1.
            // L[j][k] must have been filled
            // before as we run the loop from
            // right side
            L[i, j] = L[j, k] + 1;

            // Update overall LLAP, if needed
            llap = Math.Max(llap, L[i, j]);

            // Change i and k to fill
            // more L[i][j] values for current j
            i--; k++;
        }
        }

        // If the loop was stopped due
        // to k becoming more than
        // n-1, set the remaining
        // entities in column j as 2
        while (i >= 0)
        {
            L[i, j] = 2;
            i--;
        }
    }
    return llap;
}

// Driver Code
static public void Main ()
{
    int []set1 = {1, 7, 10, 13, 14, 19};
    int n1 = set1.Length;
    Console.WriteLine(lenghtOfLongestAP(set1, n1));

    int []set2 = {1, 7, 10, 15, 27, 29};
    int n2 = set2.Length;
    Console.WriteLine(lenghtOfLongestAP(set2, n2));

    int []set3 = {2, 4, 6, 8, 10};
    int n3 = set3.Length;
    Console.WriteLine(lenghtOfLongestAP(set3, n3)) ;
}
}

// This code is contributed by Sach_Code
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find Length of the
// Longest AP (llap) in a given sorted set.

// The code strictly implements the
// algorithm provided in the reference.

// Returns length of the longest AP
// subset in a given set
function lenghtOfLongestAP($set, $n)
{
    if ($n <= 2)
        return $n;

    // Create a table and initialize all
    // values as 2\. The value of L[i][j]
    // stores LLAP with set[i] and set[j]
    // as first two elements of AP. Only
    // valid entries are the entries where j>i
    $L[$n][$n] = array(array());
    $llap = 2; // Initialize the result

    // Fill entries in last column as 2.
    // There will always be two elements
    // in AP with last number of set as
    // second element in AP
    for ($i = 0; $i < $n; $i++)
        $L[$i][$n - 1] = 2;

    // Consider every element as
    // second element of AP
    for ($j = $n - 2; $j >= 1; $j--)
    {
        // Search for i and k for j
        $i = $j - 1;
        $k = $j + 1;
        while ($i >= 0 && $k <= $n - 1)
        {
        if ($set[$i] + $set[$k] < 2 * $set[$j])
            $k++;

        // Before changing i, set L[i][j] as 2
        else if ($set[$i] + $set[$k] > 2 * $set[$j])
        {
            $L[$i][$j] = 2;
            $i--; }

        else
        {
            // Found i and k for j, LLAP with
            // i and j as first two elements
            // is equal to LLAP with j and k
            // as first two elements plus 1.
            // L[j][k] must have been filled
            // before as we run the loop from
            // right side
            $L[$i][$j] = $L[$j][$k] + 1;

            // Update overall LLAP, if needed
            $llap = max($llap, $L[$i][$j]);

            // Change i and k to fill more
            // L[i][j] values for current j
            $i--;
            $k++;
        }
        }

        // If the loop was stopped due to k
        // becoming more than n-1, set the
        // remaining entities in column j as 2
        while ($i >= 0)
        {
            $L[$i][$j] = 2;
            $i--;
        }
    }
    return $llap;
}

// Driver Code
$set1 = array(1, 7, 10, 13, 14, 19);
$n1 = sizeof($set1);
echo lenghtOfLongestAP($set1, $n1),"\n";

$set2 = array(1, 7, 10, 15, 27, 29);
$n2 = sizeof($set2);
echo lenghtOfLongestAP($set2, $n2),"\n";

$set3 = array(2, 4, 6, 8, 10);
$n3 = sizeof($set3);
echo lenghtOfLongestAP($set3, $n3),"\n";

// This code is contributed by Sach_Code
?>
```

## java 描述语言

```
<script>
// Javascript program to find Length of the
// Longest AP (llap) in a given sorted set.
// The code strictly implements the
// algorithm provided in the reference.

    // Returns length of the longest
    // AP subset in a given set
    function lenghtOfLongestAP(set,n)
    {
        if (n <= 2)
            return n;

        // Create a table and initialize all
        // values as 2\. The value ofL[i][j] stores
        // LLAP with set[i] and set[j] as first two
        // elements of AP. Only valid entries are
        // the entries where j>i
        let L=new Array(n);
        for(let i=0;i<n;i++)
        {
            L[i]=new Array(n);
        }

        // Initialize the result
        let llap = 2;

        // Fill entries in last column as 2.
        // There will always be two elements in
        // AP with last number of set as second
        // element in AP
        for (let i = 0; i < n; i++)
        {
            L[i][n - 1] = 2;
        }
        // Consider every element as second element of AP
        for (let j = n - 2; j >= 1; j--)
        {
            // Search for i and k for j
            let i = j -1 , k = j + 1;
            while (i >= 0 && k <= n - 1)
            {
                if (set[i] + set[k] < 2 * set[j])
                    k++;

                // Before changing i, set L[i][j] as 2
                else if (set[i] + set[k] > 2 * set[j])
                {
                    L[i][j] = 2; i--;

                }

                else
                {
                    // Found i and k for j, LLAP with i and j as first two
                    // elements is equal to LLAP with j and k as first two
                    // elements plus 1\. L[j][k] must have been filled
                    // before as we run the loop from right side
                    L[i][j] = L[j][k] + 1;

                    // Update overall LLAP, if needed
                    llap = Math.max(llap, L[i][j]);

                    // Change i and k to fill
                    // more L[i][j] values for current j
                    i--; k++;
                }
            }
            // If the loop was stopped due
            // to k becoming more than
            // n-1, set the remaining
            // entities in column j as 2
            while (i >= 0)
            {
                L[i][j] = 2;
                i--;
            }
        }
        return llap;
    }

    // Driver program
    let set1=[1, 7, 10, 13, 14, 19];
    let n1 = set1.length;
    document.write( lenghtOfLongestAP(set1, n1)+"<br>");

    let set2=[1, 7, 10, 15, 27, 29];
    let n2 = set2.length;
    document.write( lenghtOfLongestAP(set2, n2)+"<br>");

    let set3=[2, 4, 6, 8, 10];
    let n3 = set3.length;
    document.write( lenghtOfLongestAP(set3, n3)+"<br>");

    // This code is contributed by avanitrachhadiya2155

</script>
```

**输出:**

```
4
3
5
```

**时间复杂度:**O(n<sup>2</sup>)
T5】辅助空间: O(n <sup>2</sup>

***如何为上述解决方案降低空间复杂度？***
我们也可以把空间复杂度降低到 **O(n)** 。
下面是空间复杂度为 **O(n)** 的动态规划算法的实现。

## C++

```
// C++ program to find Length of the
// Longest AP (llap) in a given sorted set.
#include <bits/stdc++.h>

using namespace std;

// Returns length of the longest
// AP subset in a given set
int Solution(vector<int> A)
{
    int ans = 2;
    int n = A.size();
    if (n <= 2)
        return n;

    vector<int> llap(n, 2);

    sort(A.begin(), A.end());

    for (int j = n - 2; j >= 0; j--)
    {
        int i = j - 1;
        int k = j + 1;
        while (i >= 0 && k < n)
        {
            if (A[i] + A[k] == 2 * A[j])
            {
                llap[j] = max(llap[k] + 1, llap[j]);
                ans = max(ans, llap[j]);
                i -= 1;
                k += 1;
            }
            else if (A[i] + A[k] < 2 * A[j])
                k += 1;
            else
                i -= 1;
        }
    }
    return ans;
}

// Driver Code
int main()
{
    vector<int> a({ 9, 4, 7, 2, 10 });
    cout << Solution(a) << endl;
    return 0;
}

// This code is contributed by ashutosh450
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find Length of the
// Longest AP (llap) in a given sorted set.
import java.util.*;

class GFG
{

// Returns length of the longest
// AP subset in a given set
static int Solution(int []A)
{
    int ans = 2;
    int n = A.length;
    if (n <= 2)
        return n;

    int []llap = new int[n];
    for(int i = 0; i < n; i++)
        llap[i] = 2;

    Arrays.sort(A);

    for (int j = n - 2; j >= 0; j--)
    {
        int i = j - 1;
        int k = j + 1;
        while (i >= 0 && k < n)
        {
            if (A[i] + A[k] == 2 * A[j])
            {
                llap[j] = Math.max(llap[k] + 1, llap[j]);
                ans = Math.max(ans, llap[j]);
                i -= 1;
                k += 1;
            }
            else if (A[i] + A[k] < 2 * A[j])
                k += 1;
            else
                i -= 1;
        }
    }
    return ans;
}

// Driver Code
public static void main(String[] args)
{
    int []a = { 9, 4, 7, 2, 10 };
    System.out.print(Solution(a) +"\n");
}
}

// This code is contributed by Rajput-Ji
```

## 计算机编程语言

```
# Python program to find Length 
# of the Longest AP (llap) in a given sorted set.

 # Returns length of the longest AP subset in a given set

class Solution:
    def Solve(self, A):
        ans = 2       
        n= len(A)
        if n<=2 :
            return n
        llap = [2]*n
        A.sort()

        for j in range(n-2, -1, -1):
            i= j-1
            k= j+1
            while(i>=0 and k<n):
                if A[i]+A[k] == 2*A[j]:
                    llap[j] = max(llap[k]+1,llap[j])
                    ans = max(ans, llap[j])
                    i-=1
                    k+=1
                elif A[i]+A[k] < 2*A[j]:
                    k += 1
                else:
                    i -= 1

        return ans 

# Driver program to test above function
obj = Solution()
a= [9, 4, 7, 2, 10]
print(obj.Solve(a))
```

## C#

```
// C# program to find Length of the
// longest AP (llap) in a given sorted set.
using System;

class GFG
{

// Returns length of the longest
// AP subset in a given set
static int Solution(int []A)
{
    int ans = 2;
    int n = A.Length;
    if (n <= 2)
        return n;

    int []llap = new int[n];
    for(int i = 0; i < n; i++)
        llap[i] = 2;

    Array.Sort(A);

    for (int j = n - 2; j >= 0; j--)
    {
        int i = j - 1;
        int k = j + 1;
        while (i >= 0 && k < n)
        {
            if (A[i] + A[k] == 2 * A[j])
            {
                llap[j] = Math.Max(llap[k] + 1, llap[j]);
                ans = Math.Max(ans, llap[j]);
                i -= 1;
                k += 1;
            }
            else if (A[i] + A[k] < 2 * A[j])
                k += 1;
            else
                i -= 1;
        }
    }
    return ans;
}

// Driver Code
public static void Main(String[] args)
{
    int []a = { 9, 4, 7, 2, 10 };
    Console.Write(Solution(a) +"\n");
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// Javascript program to find Length of the
// Longest AP (llap) in a given sorted set.   

    // Returns length of the longest
    // AP subset in a given set
    function Solution(A)
    {
        let ans = 2;
        let n = A.length;

        if (n <= 2)
        {
            return n;
        }

        let llap = new Array(n);
        for(let i = 0; i < n; i++)
        {
            llap[i] = 2;
        }
        A.sort(function(a, b){return a-b});
        for (let j = n - 2; j >= 0; j--)
        {
            let i = j - 1;
            let k = j + 1;
            while (i >= 0 && k < n)
            {
                if (A[i] + A[k] == (2 * A[j]))
                {
                    llap[j] = Math.max((llap[k] + 1), llap[j]);
                    ans = Math.max(ans, llap[j]);
                    i -= 1;
                    k += 1;
                }
                else if (A[i] + A[k] < 2 * A[j])
                    k += 1;
                else
                    i -= 1;
            }
        }
        return ans;
    }
    // Driver Code

    let a=[9, 4, 7, 2, 10 ];
    document.write(Solution(a) +"<br>");

    // This code is contributed by rag2127

</script>
```

**输出:**

```
3
```

**时间复杂度:**O(n)<sup>2</sup>)
**辅助空间:** O(n)
以上解决方案由乌蒙古普塔提交

**参考文献:**
[【http://www.cs.uiuc.edu/~jeffe/pubs/pdf/arith.pdf】](http://www.cs.uiuc.edu/~jeffe/pubs/pdf/arith.pdf)
如发现有不正确的地方，或想分享以上讨论话题的更多信息，请写评论