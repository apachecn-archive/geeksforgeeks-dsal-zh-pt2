# 给定原始字符串中有序三元组(R，G，B)的计数

> 原文:[https://www . geesforgeks . org/有序三元组计数-r-g-b-in-a-给定原始字符串/](https://www.geeksforgeeks.org/count-of-ordered-triplets-r-g-b-in-a-given-original-string/)

给定一个大小为 **N** 的字符串 **S** ，任务是统计给定字符串中所有可能的三元组，该字符串仅由 3 种颜色组成，依次为 **(R，G，B)** 。

**示例:**

> **输入:**S = " RRGB "
> T3】输出:2
> T6】说明:给定字符串中有两个 RGB 三元组:
> 
> *   索引 0 处的 r、索引 2 处的 G 和索引 3 处的 B 形成一个 RGB 三元组。
> *   索引 1 处的 r、索引 2 处的 G 和索引 3 处的 B 形成了 RGB 的第二个三元组。
> 
> **输入:**S = " GBR "
> T3】输出:0
> T6】说明:不存在三胞胎。

**进场:**

1.  计算给定字符串中的 B(蓝色)数，并将该值存储在 **Blue_Count** 变量中。
2.  初始化**红色 _ 计数** = 0。
3.  从左到右迭代字符串的所有字符。
4.  如果当前字符是(R)红色，则增加**红色 _ 计数**。
5.  如果当前字符为(B)蓝色，则减少**蓝色 _ 计数**。
6.  如果当前字符是 G(绿色)，则在结果中添加**红色 _ 计数** * **蓝色 _ 计数**。

下面是上述方法的实现。

## C++

```
// C++ code for the above program

#include <bits/stdc++.h>
using namespace std;

// function to count the
// ordered triplets (R, G, B)
int countTriplets(string color)
{
    int result = 0, Blue_Count = 0;
    int Red_Count = 0;

    // count the B(blue) colour
    for (char c : color) {
        if (c == 'B')
            Blue_Count++;
    }

    for (char c : color) {
        if (c == 'B')
            Blue_Count--;
        if (c == 'R')
            Red_Count++;
        if (c == 'G')
            result += Red_Count * Blue_Count;
    }
    return result;
}

// Driver program
int main()
{
    string color = "RRGGBBRGGBB";
    cout << countTriplets(color);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java code for the above program
class GFG{

// function to count the
// ordered triplets (R, G, B)
static int countTriplets(String color)
{
    int result = 0, Blue_Count = 0;
    int Red_Count = 0;
    int len = color.length();
    int i;

    // count the B(blue) colour
    for (i = 0; i < len ; i++)
    {
        if (color.charAt(i) == 'B')
            Blue_Count++;
    }

    for (i = 0; i < len ; i++)
    {
        if (color.charAt(i) == 'B')
            Blue_Count--;
        if (color.charAt(i) == 'R')
            Red_Count++;
        if (color.charAt(i) == 'G')
            result += Red_Count * Blue_Count;
    }
    return result;
}

// Driver Code
public static void main (String[] args)
{
    String color = "RRGGBBRGGBB";
    System.out.println(countTriplets(color));
}

}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 code for the above program

# function to count the
# ordered triplets (R, G, B)
def countTriplets(color) :

    result = 0; Blue_Count = 0;
    Red_Count = 0;

    # count the B(blue) colour
    for c in color :
        if (c == 'B') :
            Blue_Count += 1;

    for c in color :
        if (c == 'B') :
            Blue_Count -= 1;

        if (c == 'R') :
            Red_Count += 1;

        if (c == 'G') :
            result += Red_Count * Blue_Count;

    return result;

# Driver Code
if __name__ == "__main__" :

    color = "RRGGBBRGGBB";
    print(countTriplets(color));

# This code is contributed by AnkitRai01
```

## C#

```
// C# code for the above program
using System;
class GFG{

// function to count the
// ordered triplets (R, G, B)
static int countTriplets(String color)
{
    int result = 0, Blue_Count = 0;
    int Red_Count = 0;
    int len = color.Length;
    int i;

    // count the B(blue) colour
    for (i = 0; i < len ; i++)
    {
        if (color[i] == 'B')
            Blue_Count++;
    }

    for (i = 0; i < len ; i++)
    {
        if (color[i] == 'B')
            Blue_Count--;
        if (color[i] == 'R')
            Red_Count++;
        if (color[i] == 'G')
            result += Red_Count * Blue_Count;
    }
    return result;
}

// Driver Code
public static void Main(string[] args)
{
    string color = "RRGGBBRGGBB";
    Console.WriteLine(countTriplets(color));
}
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// Javascript code for the above program

// function to count the
// ordered triplets (R, G, B)
function countTriplets(color)
{
    var result = 0, Blue_Count = 0;
    var Red_Count = 0;

    var data = color.split('');

    // count the B(blue) colour
    for (var i=0;i<data.length;i++)
    {
        if (data[i] == 'B')
            Blue_Count++;
    }

    for (var i=0;i<data.length;i++){
        if (data[i] == 'B')
            Blue_Count--;
        if (data[i] == 'R')
            Red_Count++;
        if (data[i] == 'G')
            result += Red_Count * Blue_Count;
    }
    return result;
}

// Driver program
var color = "RRGGBBRGGBB";
document.write( countTriplets(color));

</script>
```

**Output:** 

```
28
```

**时间复杂度:***O(N)*
T5】辅助空间复杂度: *O(1)*