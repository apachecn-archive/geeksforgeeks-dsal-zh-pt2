# 使用包含至少 2 个不同字符的给定字符对 3 个长度字符串进行计数

> 原文:[https://www . geesforgeks . org/3 长度字符串计数-使用给定字符-包含至少 2 个不同字符/](https://www.geeksforgeeks.org/count-of-3-length-strings-using-given-characters-containing-at-least-2-different-characters/)

给定三个整数 **a** 、 **b** 和 **c** ，分别表示三个不同字符的频率“ **A** ”、“ **B** ”和“ **C** ”，可以组成长度为 3 的字符串。任务是计算 A、B 和 C 的可能组合的总数，使其形成至少有 **2** **个不同**字符的字符串。

**示例:**

> **输入:** a = 2，b = 3，c = 3
> **输出:** 2
> **说明:**满足给定条件的可能字符串有:{“ABC”、“ABC”}
> 
> **输入:** a = 5，b = 4，c = 3
> T3】输出: 4

**方法:**长度为 3 的字符串的总数，在给定的频率下可以形成为 **(a+b+c)/3，**假设为任意字符串选择任意字符。但是因为只需要两个不同字符的字符串，所以检查这是否可能是很重要的。要检查:

1.  假设所有 **(a+b+c)/3** 字符串最多只形成两个位置，并且所有字符串都有剩余空间需要填充。
2.  到目前为止，字符串是有效的，因为:
    *   如果字符串有两个不同的字符，那么它就是有效的。
    *   如果字符串有两个相同的字符，则可以通过插入不同的字符使其有效。
3.  因此，我们需要的不同字符的总数是，假设每个字符串需要一个字符，假设**计数**，其中**计数= (a+b+c)/3** 。
4.  所以如果两个最小频率之和超过**计数**，那么就可以形成 **(a+b+c)/3** 个数的弦。否则，它将是两个最小频率的总和。

下面是上述方法的实现:

## C++

```
// C++ implementation for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to count possible number of strings
// such that each string consists of atleast
// 2 different characters of length 3
int countStrings(int a, int b, int c)
{
    // Array to store the 3 frequencies
    int arr[3];

    arr[0] = a;
    arr[1] = b;
    arr[2] = c;

    // Total number of strings that can be
    // formed irrespective of the given
    // condition i.e, neglecting the condition
    // that each string consists of atleast 2
    // different characters of length 3
    int count = (arr[0] + arr[1] + arr[2]) / 3;

    // Sort the array
    sort(arr, arr + 3);

    // If the sum of smallest and 2nd largest
    // element is less than the count, then
    // assign the sum to count
    if (arr[0] + arr[1] < count) {
        count = arr[0] + arr[1];
    }

    // Return the count
    return count;
}

// Driver Code
int main()
{
    int a = 5, b = 4, c = 3;

    cout << countStrings(a, b, c);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation for the above approach
import java.util.*;

class GFG
{
    // Function to count possible number of strings
    // such that each string consists of atleast
    // 2 different characters of length 3
    public static int countStrings(int a, int b, int c)
    {

        // Array to store the 3 frequencies
        int[] arr = new int[3];

        arr[0] = a;
        arr[1] = b;
        arr[2] = c;

        // Total number of strings that can be
        // formed irrespective of the given
        // condition i.e, neglecting the condition
        // that each string consists of atleast 2
        // different characters of length 3
        int count = (arr[0] + arr[1] + arr[2]) / 3;

        // Sort the array
        Arrays.sort(arr);

        // If the sum of smallest and 2nd largest
        // element is less than the count, then
        // assign the sum to count
        if (arr[0] + arr[1] < count) {
            count = arr[0] + arr[1];
        }

        // Return the count
        return count;
    }

    // Driver Code
    public static void main(String[] args) {

        int a = 5, b = 4, c = 3;

        System.out.println(countStrings(a, b, c));
    }
}

// This code is contributed by Samim Hossain Mondal
```

## 蟒蛇 3

```
# Python3 implementation for the above approach

# Function to count possible number of strings
# such that each string consists of atleast
# 2 different characters of length 3
def countStrings(a, b, c) :

    # Array to store the 3 frequencies
    arr = [0]*3;

    arr[0] = a;
    arr[1] = b;
    arr[2] = c;

    # Total number of strings that can be
    # formed irrespective of the given
    # condition i.e, neglecting the condition
    # that each string consists of atleast 2
    # different characters of length 3
    count = (arr[0] + arr[1] + arr[2]) // 3;

    # Sort the array
    arr.sort();

    # If the sum of smallest and 2nd largest
    # element is less than the count, then
    # assign the sum to count
    if (arr[0] + arr[1] < count) :
        count = arr[0] + arr[1];

    # Return the count
    return count;

# Driver Code
if __name__ == "__main__" :

    a = 5; b = 4; c = 3;

    print(countStrings(a, b, c));

    # This code is contributed by AnkThon
```

## C#

```
// C# code for the above approach
using System;

public class GFG
{

    // Function to count possible number of strings
    // such that each string consists of atleast
    // 2 different characters of length 3
    public static int countStrings(int a, int b, int c)
    {

        // Array to store the 3 frequencies
        int[] arr = new int[3];

        arr[0] = a;
        arr[1] = b;
        arr[2] = c;

        // Total number of strings that can be
        // formed irrespective of the given
        // condition i.e, neglecting the condition
        // that each string consists of atleast 2
        // different characters of length 3
        int count = (arr[0] + arr[1] + arr[2]) / 3;

        // Sort the array
        Array.Sort(arr);

        // If the sum of smallest and 2nd largest
        // element is less than the count, then
        // assign the sum to count
        if (arr[0] + arr[1] < count) {
            count = arr[0] + arr[1];
        }

        // Return the count
        return count;
    }

    // Driver Code
    static public void Main()
    {

        // Code
        int a = 5, b = 4, c = 3;

        Console.Write(countStrings(a, b, c));
    }
}

// This code is contributed by Potta Lokesh
```

## java 描述语言

```
<script>

// Javascript implementation for the above approach

// Function to count possible number of strings
// such that each string consists of atleast
// 2 different characters of length 3
function countStrings(a, b, c)
{
    // Array to store the 3 frequencies
    var arr = [0,0,0];

    arr[0] = a;
    arr[1] = b;
    arr[2] = c;

    // Total number of strings that can be
    // formed irrespective of the given
    // condition i.e, neglecting the condition
    // that each string consists of atleast 2
    // different characters of length 3
    var count = parseInt((arr[0] + arr[1] + arr[2]) / 3);

    // Sort the array
    arr.sort((a,b) => a-b);

    // If the sum of smallest and 2nd largest
    // element is less than the count, then
    // assign the sum to count
    if (arr[0] + arr[1] < count) {
        count = arr[0] + arr[1];
    }

    // Return the count
    return count;
}

// Driver Code
var a = 5, b = 4, c = 3;
document.write(countStrings(a, b, c));

// This code is contributed by rutvik_56.
</script>
```

**Output**

```
4
```

**时间复杂度:**O(1)
T3】辅助空间: O(1)