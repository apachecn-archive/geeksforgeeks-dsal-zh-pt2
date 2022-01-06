# 根据位数总和分组时最大组数

> 原文:[https://www . geeksforgeeks . org/按数字总和分组时拥有最大大小的组数/](https://www.geeksforgeeks.org/count-of-groups-having-largest-size-while-grouping-according-to-sum-of-its-digits/)

给定一个整数 **N** ，任务是找到具有最大大小的组的数量。从 **1 到 N** 的每个数字根据其数字的**总和进行分组。**

**示例:**

> **输入:** N = 13
> **输出:** 4
> **说明:**
> 共 9 组，按其数字位数之和从 1 到 13 进行分组:[1，10] [2，11] [3，12] [4，13] [5] [6] [7] [8] [9]。
> 其中，4 组规模最大，为 2 组。
> 
> **输入:** n = 2
> **输出:** 2
> **说明:**
> 共 2 组。[1] [2]并且两个组都具有最大尺寸 1。

**方法:**为了解决上面提到的问题，我们需要创建一个[字典](https://www.geeksforgeeks.org/python-dictionary/)，其关键字代表从 1 到 N 的数字的唯一[和](https://www.geeksforgeeks.org/count-sum-of-digits-in-numbers-from-1-to-n/)。这些键的值将继续计算有多少数字的和等于它的键。然后我们将打印其中最高的值。

**以下是上述方法的实现:**

## C++

```
// C++ implementation to Count the
// number of groups having the largest
// size where groups are according
// to the sum of its digits
#include <bits/stdc++.h>
using namespace std;

// function to return sum of digits of i
int sumDigits(int n){
    int sum = 0;
    while(n)
    {
        sum += n%10;
        n /= 10;
    }

    return sum;
}

// Create the dictionary of unique sum
map<int,int> constDict(int n){

    // dictionary that contain
    // unique sum count
    map<int,int> d;

    for(int i = 1; i < n + 1; ++i){
        // calculate the sum of its digits
        int sum1 = sumDigits(i);

        if(d.find(sum1) == d.end())
            d[sum1] = 1;
        else
            d[sum1] += 1;       
    }

    return d;
}

// function to find the
// largest size of group
int countLargest(int n){

    map<int,int> d = constDict(n);

    int size = 0;

    // count of largest size group
    int count = 0;

    for(auto it = d.begin(); it != d.end(); ++it){
        int k = it->first;
        int val = it->second;

        if(val > size){           
            size = val;
            count = 1;
        }
        else if(val == size)           
            count += 1;
    }

    return count;
}

// Driver code
int main()
{
    int    n = 13;

    int group = countLargest(n);

    cout << group << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to Count the 
// number of groups having the largest 
// size where groups are according 
// to the sum of its digits
import java.util.HashMap;
import java.util.Map;

class GFG{

// Function to return sum of digits of i
public static int sumDigits(int n)
{
    int sum = 0;
    while(n != 0)
    {
        sum += n % 10;
        n /= 10;
    }

    return sum;
}

// Create the dictionary of unique sum 
public static HashMap<Integer, Integer> constDict(int n)
{

    // dictionary that contain 
    // unique sum count 
    HashMap<Integer, Integer> d = new HashMap<>();

    for(int i = 1; i < n + 1; ++i)
    {

        // Calculate the sum of its digits 
        int sum1 = sumDigits(i);

        if (!d.containsKey(sum1))
            d.put(sum1, 1);
        else
            d.put(sum1, d.get(sum1) + 1);
    }
    return d;
}

// Function to find the 
// largest size of group 
public static int countLargest(int n)
{
    HashMap<Integer, Integer> d = constDict(n); 

    int size = 0;

    // Count of largest size group 
    int count = 0;

    for(Map.Entry<Integer, Integer> it : d.entrySet())
    {
        int k = it.getKey();
        int val = it.getValue();

        if (val > size)
        {            
            size = val;
            count = 1;
        }
        else if (val == size)            
            count += 1;
    }

    return count;
}

// Driver code
public static void main(String[] args)
{
    int n = 13;
    int group = countLargest(n); 

    System.out.println(group);
}
}

// This code is contributed by divyeshrabadiya07
```

## 蟒蛇 3

```
# Python3 implementation to Count the
# number of groups having the largest
# size where groups are according
# to the sum of its digits

# Create the dictionary of unique sum
def constDict(n):

    # dictionary that contain
    # unique sum count
    d ={}

    for i in range(1, n + 1):

        # convert each number to string
        s = str(i)

        # make list of number digits
        l = list(s)

        # calculate the sum of its digits
        sum1 = sum(map(int, l))

        if sum1 not in d:
            d[sum1] = 1

        else:
            d[sum1] += 1

    return d

# function to find the
# largest size of group
def countLargest(n):

    d = constDict(n)

    size = 0

    # count of largest size group
    count = 0

    for k, val in d.items():

        if val > size:

            size = val
            count = 1

        elif val == size:

            count += 1

    return count

# Driver Code
n = 13
group = countLargest(n)
print(group)

# This code is contributed by Sanjit_Prasad
```

## C#

```
// C# implementation to Count the 
// number of groups having the largest 
// size where groups are according 
// to the sum of its digits
using System;
using System.Collections.Generic;
class GFG {

    // Function to return sum of digits of i
    static int sumDigits(int n)
    {
        int sum = 0;
        while(n != 0)
        {
            sum += n % 10;
            n /= 10;
        }

        return sum;
    }

    // Create the dictionary of unique sum 
    static Dictionary<int, int> constDict(int n)
    {

        // dictionary that contain 
        // unique sum count 
        Dictionary<int, int> d = new Dictionary<int, int>();

        for(int i = 1; i < n + 1; ++i)
        {

            // Calculate the sum of its digits 
            int sum1 = sumDigits(i);

            if (!d.ContainsKey(sum1))
                d.Add(sum1, 1);
            else
                d[sum1] += 1;
        }
        return d;
    }

    // Function to find the 
    // largest size of group 
    static int countLargest(int n)
    {
        Dictionary<int, int> d = constDict(n); 

        int size = 0;

        // Count of largest size group 
        int count = 0;

        foreach(KeyValuePair<int, int> it in d)
        {
            int k = it.Key;
            int val = it.Value;

            if (val > size)
            {            
                size = val;
                count = 1;
            }
            else if (val == size)            
                count += 1;
        }

        return count;
    }  

  // Driver code
  static void Main()
  {
    int n = 13;
    int group = countLargest(n); 
    Console.WriteLine(group);
  }
}

// This code is contributed by divyesh072019
```

**Output:** 

```
4
```

***时间复杂度:** O(N)*

***辅助空间:**O(N)*T4】