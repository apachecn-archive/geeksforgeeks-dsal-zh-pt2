# 数组和映射的区别

> 原文:[https://www . geesforgeks . org/数组和映射的区别/](https://www.geeksforgeeks.org/difference-between-array-and-map/)

### **阵列:**

[数组](https://www.geeksforgeeks.org/array-data-structure/)是存储在连续存储位置的项目的集合。想法是将多个相同类型的项目存储在一起。这使得通过简单地将偏移加到基值，即数组的第一个元素的存储位置(通常由数组的名称表示)，来计算每个元素的位置变得更容易。
阵列的图示如下:

[![](img/f135b70319b69f7c8fc3364f232504ba.png)](https://media.geeksforgeeks.org/wp-content/uploads/Arrays-1.png)

**程序 1:**
下面是一个 1D 阵的图解:

## C++

```
// C++ program to illustrate 1D array
#include <bits/stdc++.h>
using namespace std;

// Driver Code
int main()
{
    // Given array
    int arr[] = { 6, 10, 5, 0 };

    // Print the array elements
    for (int i = 0; i < 4; i++) {
        cout << arr[i] << " ";
    }

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to illustrate 1D array
class GFG{

// Driver Code
public static void main(String[] args)
{
    // Given array
    int arr[] = { 6, 10, 5, 0 };

    // Print the array elements
    for (int i = 0; i < 4; i++)
    {
        System.out.print(arr[i] + " ");
    }
}
}

// This code is contributed by Rohit_ranjan
```

## 蟒蛇 3

```
# Python3 program to illustrate 1D array

# Driver Code
if __name__ == '__main__':

    # Given array
    arr = [6, 10, 5, 0];

    # Print the array elements
    for i in range(0, 4):
        print(arr[i], end = " ");

# This code is contributed by Rohit_ranjan
```

## C#

```
// C# program to illustrate 1D array
using System;
class GFG{

    // Driver Code
    public static void Main(String[] args)
    {

        // Given array
        int[] arr = {6, 10, 5, 0};

        // Print the array elements
        for (int i = 0; i < 4; i++)
        {
            Console.Write(arr[i] + " ");
        }
    }
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
    // Javascript program to illustrate 1D array

    // Given array
    let arr = [6, 10, 5, 0];

    // Print the array elements
    for (let i = 0; i < 4; i++)
    {
      document.write(arr[i] + " ");
    }

// This code is contributed by divyeshrabadiya07.
</script>
```

**Output:** 

```
6 10 5 0
```