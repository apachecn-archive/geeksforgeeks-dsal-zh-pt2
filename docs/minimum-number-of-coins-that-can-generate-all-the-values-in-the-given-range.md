# 能产生给定范围内所有数值的最小硬币数

> 原文:[https://www . geesforgeks . org/能产生给定范围内所有值的最小硬币数/](https://www.geeksforgeeks.org/minimum-number-of-coins-that-can-generate-all-the-values-in-the-given-range/)

给定一个整数 **N** ，任务是找到创建范围**【1，N】**中所有值所需的最小硬币数。

**示例:**

```
Input: N = 5
Output: 3
The coins {1, 2, 4} can be used to generate 
all the values in the range [1, 5].
1 = 1
2 = 2
3 = 1 + 2
4 = 4
5 = 1 + 4

Input: N = 10
Output: 4
```

**进场:**问题是硬币兑换问题的一个变种，可以借助二进制数来解决。在上例中，可以看到要创建 **1** 到 **10** 之间的所有值，需要分母 **{1，2，4，8}** ，可以改写为 **{2 <sup>0</sup> ，2 <sup>1</sup> ，2 <sup>2</sup> ，2 <sup>3</sup> }** 。为一个值 **N** 创建所有值的最小硬币数量可以使用以下算法计算。

```
// A list which contains the sum of all previous 
// bit values including that bit value
list = [ 1, 3, 7, 15, 31, 63, 127, 255, 511, 1023]
    // range = N
    for value in  list:
        if(value >= N):
            print(list.index(value) + 1)
            break
```

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

int index(vector<int> vec, int value)
{
    vector<int>::iterator it;
    it = find(vec.begin(), vec.end(), value);
    return (it - vec.begin());
}

// Function to return the count
// of minimum coins required
int findCount(int N)
{

    // To store the required sequence
    vector<int> list;
    int sum = 0;
    int i;

    // Creating list of the sum of all
    // previous bit values including
    // that bit value
    for (i = 0; i < 20; i++) {
        sum += pow(2, i);
        list.push_back(sum);
    }

    for (i = 0; i < 20; i++) {
        if (list[i] >= N) {
            return (index(list, list[i]) + 1);
        }
    }
}

// Driver Code
int main()
{
    int N = 10;
    cout << findCount(N) << endl;
    return 0;
}

// This code is contributed by kanugargng
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG {

    // Function to return the count
    // of minimum coins required
    static int findCount(int N)
    {
        Vector list = new Vector();
        int sum = 0;
        int i;

        // Creating list of the sum of all
        // previous bit values including
        // that bit value
        for (i = 0; i < 20; i++) {
            sum += Math.pow(2, i);
            list.add(sum);
        }

        for (i = 0; i < 20; i++) {
            if ((int)list.get(i) >= N)
                return (list.indexOf(list.get(i)) + 1);
        }
        return 0;
    }

    // Driver Code
    public static void main(String[] args)
    {
        int N = 10;

        // Function Call to find count
        System.out.println(findCount(N));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count
# of minimum coins required

def findCount(N):

    # To store the required sequence
    list = []
    sum = 0

    # Creating list of the sum of all
    # previous bit values including
    # that bit value
    for i in range(0, 20):
        sum += 2**i
        list.append(sum)

    for value in list:
        if(value >= N):
            return (list.index(value) + 1)

# Driver code
N = 10
print(findCount(N))
```

## C#

```
// C# implementation of the above approach
using System;
using System.Collections.Generic;

class GFG {

    // Function to return the count
    // of minimum coins required
    static int findCount(int N)
    {
        List<int> list = new List<int>();
        int sum = 0;
        int i;

        // Creating list of the sum of all
        // previous bit values including
        // that bit value

        for (i = 0; i < 20; i++) {
            sum += (int)Math.Pow(2, i);
            list.Add(sum);
        }

        for (i = 0; i < 20; i++) {
            if ((int)list[i] >= N)
                return (i + 1);
        }
        return 0;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int N = 10;
        Console.WriteLine(findCount(N));
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
    // Javascript implementation of the above approach

    // Function to return the count
    // of minimum coins required
    function findCount(N)
    {
        let list = [];
        let sum = 0;
        let i;

        // Creating list of the sum of all
        // previous bit values including
        // that bit value

        for (i = 0; i < 20; i++) {
            sum += parseInt(Math.pow(2, i), 10);
            list.push(sum);
        }

        for (i = 0; i < 20; i++) {
            if (list[i] >= N)
                return (i + 1);
        }
        return 0;
    }

    let N = 10;
      document.write(findCount(N));

    // This code is contributed by rameshtravel07.
</script>
```

**Output**

```
4
```

**时间复杂度:** O(n)

**有效方法:**创建范围**【1，N】**中所有值所需的最小硬币数将为 **log(N)/log(2) + 1。**

下面是上述方法的实现:

## C++14

```
// C++ program to find minimum number of coins
#include<bits/stdc++.h>
using namespace std;

// Function to find minimum number of coins
int findCount(int n)
{
    return log(n)/log(2)+1;
}

// Driver code
int main()
{
    int N = 10;
    cout << findCount(N) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find minimum number of coins
class GFG{

// Function to find minimum number of coins
static int findCount(int n)
{
    return (int)(Math.log(n) /
                 Math.log(2)) + 1;
}

// Driver code
public static void main(String[] args)
{
    int N = 10;

    System.out.println(findCount(N));
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 program to find minimum number of coins
import math

# Function to find minimum number of coins
def findCount(n):

    return int(math.log(n, 2)) + 1

# Driver code
N = 10

print(findCount(N))

# This code is contributed by divyesh072019
```

## C#

```
// C# program to find minimum number of coins
using System;

class GFG{

  // Function to find minimum number of coins
  static int findCount(int n)
  {
    return (int)(Math.Log(n) /
                 Math.Log(2)) + 1;
  }

  // Driver code
  public static void Main()
  {
    int N = 10;

    Console.Write(findCount(N));
  }
}

// This code is contributed by rutvik_56.
```

## java 描述语言

```
<script>
    // Javascript program to find minimum number of coins

    // Function to find minimum number of coins
    function findCount(n)
    {
        return parseInt(Math.log(n)/Math.log(2), 10)+1;
    }

    let N = 10;
    document.write(findCount(N));

</script>
```

**Output**

```
4
```

**时间复杂度:** O(log(n))